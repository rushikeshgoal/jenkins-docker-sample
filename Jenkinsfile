pipeline {
    agent any

    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
    IMAGE_NAME = "rushikeshdoc/sample-app"   
}

    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }
}

