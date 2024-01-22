pipeline {
    agent any

    stages {
        stage('DEV') {
            steps {
                echo 'Building..'
                sh 'npm install'
                sh '<<Build Command>>'
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