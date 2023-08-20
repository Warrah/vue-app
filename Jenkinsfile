pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                // Copy the built project to the Nginx web server directory
echo 123 | sudo -S cp -r dist/css dist/favicon.ico dist/index.html dist/js /var/www/html/

                // Reload Nginx to apply changes
                sh 'sudo systemctl reload nginx'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
