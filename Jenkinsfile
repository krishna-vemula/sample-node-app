pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = '9c466563-3bac-40fc-b02c-21807090079c'  // Jenkins GitHub credentials ID
        DOCKER_IMAGE = 'sample-node-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'https://github.com/krishna-vemula/sample-node-app.git',
                    credentialsId: "${GIT_CREDENTIALS}",
                    branch: 'main'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build || echo "No build step defined"'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p 3000:3000 ${DOCKER_IMAGE}"
            }
        }

        stage('Success') {
            steps {
                echo '✅ Application built, tested, and running in Docker!'
            }
        }
    }
}
