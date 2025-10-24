pipeline {
    agent any
    environment {
        // Jenkins मध्ये add केलेले DockerHub credentials ID = 'dockerhub'
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        IMAGE_NAME = "rushikeshdoc/sample-app"   // DockerHub username/repo
        IMAGE_TAG  = "latest"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image $IMAGE_NAME:$IMAGE_TAG"
                sh "docker build -t $IMAGE_NAME:$IMAGE_TAG ."
            }
        }
        stage('Login to DockerHub') {
            steps {
                echo "Logging in to DockerHub as rushikeshdoc"
                sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
            }
        }
        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to DockerHub"
                sh "docker push $IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }
    post {
        always {
            echo "Pipeline finished"
        }
        success {
            echo "✅ Docker image pushed successfully!"
        }
        failure {
            echo "❌ Pipeline failed! Check console output."
        }
    }
}

