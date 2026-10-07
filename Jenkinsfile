pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t lab1-web:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop lab1-web || true
                    docker rm lab1-web || true

                    docker run -d \
                        --name lab1-web \
                        -p 80:80 \
                        lab1-web:${BUILD_NUMBER}
                '''
            }
        }
    }
}
