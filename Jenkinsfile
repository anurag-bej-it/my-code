pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Check Docker access') {
            steps {
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker build -t my-code:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy container') {
            steps {
                sh 'docker rm -f my-code || true'

                sh 'docker run -d --name my-code -p 127.0.0.1:8080:3000 --restart unless-stopped my-code:${BUILD_NUMBER}'
            }
        }

        stage('Verify app') {
            steps {
                sh 'sleep 3'

                sh 'curl --fail --silent --show-error http://127.0.0.1:8080/ -o /dev/null'

                sh 'curl --fail --silent --show-error http://localhost/ -o /dev/null'
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded. Visit http://localhost'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}