pipeline {
    agent any
    

    // tools {
    //     nodejs '21.6.1'
    // }

    stages {

        stage('Install packages') {
            steps
                // nodejs('install nodejs') {
                sh 'npm install'
                }
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