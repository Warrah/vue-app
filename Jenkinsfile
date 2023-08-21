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
        stage('Test') {
            steps {
               echo 'Testing.......'
            }
        }

        stage('Deploy to Nginx') {
            steps {
               script {
                    echo 'Copying files to Nginx...'
                    sh 'echo 123 | sudo -S cp -r dist/css dist/favicon.ico dist/index.html dist/js /var/www/html/vue/dist'
                }

                // Reload Nginx to apply changes
                sh 'sudo systemctl reload nginx'
            }
        }
    }

    post {
        success {
        echo 'Deployment successful!'
        slackSend(
            channel: '#jenkins_personal', // Specify the Slack channel or user to send notifications to
            color: 'good',
            message: "Deployment of your vue project was successful! See localhost:8100"
        )
    }
    failure {
        echo 'Deployment failed!'
        slackSend(
            channel: '#jenkins_personal', // Specify the Slack channel or user to send notifications to
            color: 'danger',
            message: "Deployment of your vue project failed."
        )
    }
    }
}
