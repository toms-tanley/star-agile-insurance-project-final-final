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
                    sh 'mvn test'
                }
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t insurance123:v7 .' // Build Docker image
            }
        }

        stage('Deploy to the Test Server') {
            steps {
                sh 'docker run -d -p 8082:8081 insurance123:v7' // Run Docker container
                echo "Application is successfully running"
                sh 'docker rm -f $(docker ps -a -q)' // Stopping the Running Docker container
            }
        }

        stage('Docker Login') {
            steps {
                echo 'Docker Login'
                withCredentials([usernamePassword(credentialsId: 'Dockerlogin', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                }
            }
        }

        stage('Push Docker Image to Hub') {
            steps {
                echo 'Push a Docker Image'
                sh 'docker tag insurance123 thomasdevops003/insurance123'
                sh 'docker push thomasdevops003/insurance123'
                sh 'docker rmi -f $(docker images -aq)' // Cleaning up the Image
            }
        }
    }
}
