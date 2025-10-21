pipeline {
    agent none   // We specificeren per stage de agent

    stages {
        stage('Checkout on Controller') {
            agent { label 'master' }  // Controller node
            steps {
                echo 'Checkout repository on controller...'

                // GitHub public repo, dus geen credentials nodig
                checkout([$class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [[url: 'https://github.com/liquid-design/blog.git']]
                ])

                // Optioneel: verwijder oude .git info
                sh 'rm -rf .git'

                // Stash de volledige workspace zodat agents het kunnen ontvangen
                stash includes: '**/*', name: 'source'
            }
        }

        stage('Deploy to web-01') {
            agent { label 'web-01' }  // Agent node
            steps {
                echo 'Deploy code to web-01...'

                // Haal de code van de controller binnen
                unstash 'source'

                // Deploy: copy naar webroot
                sh 'sudo cp -r * /var/www/html/'
            }
        }

        stage('Deploy to web-02') {
            agent { label 'web-02' }  // Tweede agent node
            steps {
                echo 'Deploy code to web-02...'

                unstash 'source'
                sh 'rm -rf /var/www/html/*'
                sh 'sudo cp -r * /var/www/html/'
            }
        }
    }
}
