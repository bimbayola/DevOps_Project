pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/bimbayola/DevOps_Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("bimbayola/app.py")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    dockerImage.run('-d --name my_app_container')
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Możesz tu dodać kroki do testowania aplikacji
                    echo 'Testing...'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'docker stop my_app_container'
                        sh 'docker rm my_app_container'
                    }
                }
            }
        }
    }
}
