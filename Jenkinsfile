pipeline {
    agent any

    environment {
        IMAGE_NAME = "ecommerce-backend"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME ./backend'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop backend || true
                docker rm backend || true
                docker run -d \
                  --name backend \
                  -p 3000:3000 \
                  -e DB_HOST=$DB_HOST \
                  -e DB_USER=$DB_USER \
                  -e DB_PASS=$DB_PASS \
                  -e DB_NAME=$DB_NAME \
                  $IMAGE_NAME
                '''
            }
        }
    }
}
