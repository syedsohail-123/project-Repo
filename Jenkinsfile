pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "syedsohail746/age-calculator:1"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/syedsohail-123/project-Repo.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials-id') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                script {
                    sh "docker stop age-calculator-container || true"
                    sh "docker rm age-calculator-container || true"
                    sh "docker run -d --name age-calculator-container -p 82:80 ${DOCKER_IMAGE}"
                }
            }
        }
    }
}
