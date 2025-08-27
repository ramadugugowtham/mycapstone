pipeline {
    agent any

    environment {
        INVENTORY = "/home/ubuntu/inventory.ini"
        PLAYBOOK  = "/home/ubuntu/nginx.yml"
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
                echo "Deploying to AWS..."
                ansible -i ${INVENTORY} aws -m copy -a "src=index-aws.html dest=/var/www/html/index.html owner=www-data group=www-data mode=0644"
                ansible -i ${INVENTORY} aws -m service -a "name=nginx state=restarted"
                '''
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                echo "Deploying to Azure..."
                ansible -i ${INVENTORY} azure -m copy -a "src=index-azure.html dest=/var/www/html/index.html owner=www-data group=www-data mode=0644"
                ansible -i ${INVENTORY} azure -m service -a "name=nginx state=restarted"
                '''
            }
        }

        stage('Run Playbook') {
            steps {
                sh '''
                echo "Running Ansible Playbook..."
                ansible-playbook -i ${INVENTORY} ${PLAYBOOK}
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Check AWS and Azure IPs in browser."
        }
        failure {
            echo "❌ Deployment failed! Check Jenkins logs."
        }
    }
}
