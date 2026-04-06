pipeline {
    agent any

    environment {
        IMAGE_NAME = 'harshithbcs96/harshith-2022bcs0096-lab6:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Model Metrics & Identity') {
            steps {
                echo "==============================================="
                echo " STUDENT NAME: Harshith"
                echo " ROLL NO: 2022BCS0096"
                echo "==============================================="
                echo "Reading Model Metrics..."
                sh 'cat outputs/results.json'
                echo "==============================================="
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image..."
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERHUB_PSW', usernameVariable: 'DOCKERHUB_USR')]) {
                    sh '''
                    echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin
                    docker push $IMAGE_NAME
                    '''
                }
            }
        }
    }
}
