pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ramadugugowtham/mycapstone.git'
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh '''
                ansible -i inventory.ini aws -m copy -a "src=index-aws.html dest=/var/www/html/index.html owner=www-data group=www-data mode=0644"
                ansible -i inventory.ini aws -m service -a "name=nginx state=restarted"
                '''
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                ansible -i inventory.ini azure -m copy -a "src=index-azure.html dest=/var/www/html/index.html owner=www-data group=www-data mode=0644"
                ansible -i inventory.ini azure -m service -a "name=nginx state=restarted"
                '''
            }
        }
    }
}
