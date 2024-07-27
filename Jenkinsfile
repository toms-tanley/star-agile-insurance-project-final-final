pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/toms-tanley/star-agile-insurance-project-final-final.git'
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
                    sh 'mvn test' // Run the tests
                }
            }
        }
    }
}
