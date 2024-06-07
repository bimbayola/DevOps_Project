pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/bimbayola/DevOps_Project.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("bimbayola/DevOps_Project.git")
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
