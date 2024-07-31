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
                sh 'docker build -t insurance12 .' // Build Docker image
            }
        }

        stage('Deploy to the Test Server') {
            steps {
                sh 'docker run -d -p 8082:8081 insurance12' // Run Docker container
                echo "Application is successfully running"
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
                sh 'docker tag insurance12 thomasdevops003/insure:v6'
                sh 'docker push thomasdevops003/insure:v6'
                sh 'docker rmi -f $(docker images -aq)' // Cleaning up the Image
            }
        }
    }
}
