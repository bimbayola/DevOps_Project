pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'local-python-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/bimbayola/DevOps_Project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'echo "Running tests"'
                        // Tu można dodać rzeczywiste testy, np. uruchomienie pytest
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    // Uruchom nowy kontener na serwerze
                    sh "docker run -d -p 5000:5000 --name myapp ${DOCKER_IMAGE}"
                }
            }
        }

        stage('Post-Deployment Tests') {
            steps {
                script {
                    // Przykładowe testy sprawdzające dostępność aplikacji po wdrożeniu
                    sh 'curl -f http://localhost:5000 || exit 1'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
