pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'joanna2/jenkins-pipeline-webapp'
        DOCKER_CREDENTIALS_ID = 'mitchel-2017'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Joy-it-code/CI-CD-Mastery.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                
                script {
                    docker.withRegistry('', 'mitchel-2017') {
                      sh 'docker push $DOCKER_IMAGE'
                    }
                }
 
            }
        }

        stage('Deploy Container Locally') {
            steps {
                sh 'docker run -d -p 8090:80 $DOCKER_IMAGE'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

