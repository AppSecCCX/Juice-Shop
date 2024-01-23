pipeline {
    agent any

    // tools {
    //     nodejs '21.6.1'
    // }

    stages {

        stage('node') {
            steps {
                sh 'apt-get install nodejs'
                sh 'npm i'
            }
        }

        stage('Snyk') {
            steps {
                echo 'Testing...'
                snykSecurity(
                snykInstallation: 'Juiceshop',
                snykTokenId: 'Juiceshop',
                )
        }
    }

        stage('DEV') {
            steps {
                echo 'Building..'
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