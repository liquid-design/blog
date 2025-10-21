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
            agent any  // of een specifieke agent voor deploy
            steps {
                echo 'Deploying to web servers...'

                // Kopieer naar agent via scp
                sh '''
                scp -r ./ bloguser@web-01:/var/www/html/
                scp -r ./ bloguser@web-02:/var/www/html/
                '''
            }
        }
    }
}
