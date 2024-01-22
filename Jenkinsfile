pipeline {
    agent any
        environment {
            SEMGREP_APP_TOKEN = 4397b2db11ac79b3fabc12c247406a1f036773a64a58d2d573cf5f320e311bae
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