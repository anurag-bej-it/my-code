pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Hello Jenkins') {
            steps {
                echo 'Jenkins is running.'
            }
        }

        stage('Inspect project') {
            steps {
                sh 'pwd'
                sh 'git --version'
                sh 'ls -la'
            }
        }
    }

    post {
        success {
            echo 'Phase 8 passed.'
        }

        failure {
            echo 'Phase 8 failed. Read Console Output.'
        }
    }
}
