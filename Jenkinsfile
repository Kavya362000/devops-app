pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-cicd-app"
        CONTAINER_NAME = "flask-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                echo "Cloning Repository..."
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
