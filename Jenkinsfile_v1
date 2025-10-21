pipeline {
    agent none   // Geen specifieke agent nodig voor checkout

    stages {
        stage('Checkout') {
            agent { label 'master' } // master doet het checkout
            steps {
                git branch: 'main',
                    url: 'git@github.com:liquid-design/blog.git',
                    credentialsId: 'jenkins-ssh-key'  // je Jenkins SSH key
            }
        }

        stage('Deploy') {
            agent { label 'web-01' }  // draait op de agent
            steps {
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r $WORKSPACE/* /var/www/html/
                '''
            }
        }
    }
}
