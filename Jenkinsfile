pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ramadugugowtham/mycapstone.git'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                ansible-playbook -i inventory.ini nginx.yml
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed! Check Jenkins logs."
        }
    }
}
