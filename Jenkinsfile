pipeline {
    agent any

    triggers {
        cron('0 2 * * *') // Se ejecutará todos los días a las 2 AM
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = "dy010101/desafio-13"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Ejecutar el contenedor
                    sh "docker run -d --name test_container -p 5000:5000 ${IMAGE_NAME}:${IMAGE_TAG}"
                    
                    // Esperar a que la aplicación esté lista
                    sh 'sleep 10'
                    
                    // Realizar una prueba básica
                    sh 'curl http://localhost:5000 || exit 1'
                    
                    // Detener y eliminar el contenedor de prueba
                    sh 'docker stop test_container && docker rm test_container'
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push("latest")
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Detener y eliminar el contenedor existente si existe
                    sh 'docker stop desafio-13 || true'
                    sh 'docker rm desafio-13 || true'
                    
                    // Ejecutar el nuevo contenedor
                    sh "docker run -d --name desafio-13 -p 5000:5000 ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }

    post {
        always {
            // Limpiar imágenes no utilizadas
            sh 'docker image prune -f'
        }
    }
}