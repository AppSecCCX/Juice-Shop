pipeline {
    agent any
        environment {
            SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
        }

    stages {
        stage('DEV') {
            steps {
                echo 'Building..'
                 sh 'pip3 install semgrep'
                sh 'semgrep ci'
            }
        }

        stage('TEST') {
            steps {
                echo 'Testing..'
            }
        }
        stage('PROD') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}