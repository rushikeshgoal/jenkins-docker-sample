pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub') // Jenkins मध्ये add केलेले DockerHub credentials
        IMAGE_NAME = "rushikeshdoc/sample-app"          // DockerHub username/repo
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
            }
        }
        stage('Push Docker Image') {
            steps {
                sh "docker push $IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }
}

