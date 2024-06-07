pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/your-username/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("your-username/your-repo")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'echo "Running tests"'
                        // Tu można dodać rzeczywiste testy, np. uruchomienie pytest
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    dockerImage.push()
                }
            }
        }
    }
}
