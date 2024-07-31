pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/toms-tanley/Insurance-Project-star.git'
            }
        }

        stage('Code Build') {
            steps {
                sh 'mvn clean package' // Build the application
            }
        }

        stage('Code Test') {
            steps {
                script {
                   sh 'mvn test' 
                }
                
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t insurance12:v6 .' // Build Docker image
            }
        }
    }
}
