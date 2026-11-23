
pipeline {
    agent any

    options {
        disableConcurrentBuilds()
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting latest code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Checking project files'
                sh 'test -f index.html'
                sh 'test -f style.css'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website to Nginx'

                sh '''
                    rsync -av --delete \
                    --exclude='.git/' \
                    --exclude='Jenkinsfile' \
                    ./ /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed! Check console output.'
        }
    }
}
