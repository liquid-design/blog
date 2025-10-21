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
                scp -r ./ ansible@192.168.6.10:/var/www/html/
                scp -r ./ ansible@192.168.6.27:/var/www/html/
                '''
            }
        }
    }
}
