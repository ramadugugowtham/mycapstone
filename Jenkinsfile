pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ramadugugowtham/mycapstone.git'
            }
        }

        stage('Deploy to AWS & Azure') {
            steps {
                sh '''
                ansible-playbook -i /home/ubuntu/inventory.ini ./nginx.yml
                '''
            }
        }
    }
}
