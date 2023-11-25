pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio de GitHub
                git 'https://github.com/felipemunozri/react_app.git'
            }
        }

        stage('Build and Dockerize') {
            steps {
                // Construir la imagen Docker
                script {
                    docker.build("react_app:${env.BUILD_ID}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                // Subir la imagen Docker a DockerHub
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub_id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_id') {
                            docker.image("react_app:${env.BUILD_ID}").push()
                        }
                    }
                }
            }
        }
    }
}
