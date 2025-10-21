pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:liquid-design/blog.git'
                  //  credentialsId: 'jenkins-ssh-key'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh 'echo "Simuleer build stap"'
                // bv. sh './build.sh' als je een echte build hebt
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Simuleer test stap"'
                // bv. sh './test.sh'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'echo "Simuleer deploy stap"'
                // bv. scp of ansible-playbook naar productie server
            }
        }
    }
}
