pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "deva1205/python-ci-cd:latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Deva-S-pixel9/ci-cd-sonarqube-docker.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh '''
                pip3 install -r requirements.txt
                python3 -m pytest
                '''
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-token',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $DOCKER_IMAGE
                    '''
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop python-app || true
                docker rm python-app || true
                docker run -d --name python-app -p 5000:5000 $DOCKER_IMAGE
                '''
            }
        }
    }
}
