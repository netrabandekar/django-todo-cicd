pipeline {
    agent any

    environment {
        IMAGE_NAME = "django-todo-app"
        CONTAINER_NAME = "django-todo-container"
        PORT = "8000"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'develop',
                url: 'https://github.com/netrabandekar/django-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Stop Old Container') {
            steps {
                sh """
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                """
            }
        }

        stage('Run New Container') {
            steps {
                sh """
                docker run -d --name $CONTAINER_NAME -p 8000:8000 $IMAGE_NAME
                """
            }
        }

    }

    post {
        success {
            echo '🚀 Deployment Successful on EC2!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
