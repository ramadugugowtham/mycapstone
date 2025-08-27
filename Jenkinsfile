pipeline {
    agent any

    environment {
        INVENTORY = "/home/ubuntu/inventory.ini"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ramadugugowtham/mycapstone.git'
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh '''
                ansible-playbook -i ${INVENTORY} nginx.yml --limit aws
                '''
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                ansible-playbook -i ${INVENTORY} nginx.yml --limit azure
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Check AWS & Azure web pages."
        }
        failure {
            echo "❌ Deployment failed! Check Jenkins logs."
        }
    }
}
