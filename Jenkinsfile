pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent { label 'master' } // draait op Jenkins zelf
            steps {
                echo "Cloning repo on controller..."
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/liquid-design/blog.git']]
                ])
                // Bewaar code voor volgende stages
                stash name: 'source'
            }
        }

        stage('Deploy to web-01') {
            agent { label 'web-01' } // draait op de agent via WebSocket
            steps {
                echo "Preparing deployment on web-01..."
                // Haal code op uit stash
                unstash 'source'
                // Simuleer deploy (pas dit pad aan voor jouw website)
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo mkdir -p /var/www/html
                    sudo cp -r * /var/www/html/
                '''
                echo "✅ Deployment complete on web-01!"
            }
        }
    }
}
