pipeline {
    agent any

    //  tools {
    //     nodejs '21.6.1'
    // }

    stages {
        stage('Install packages') {
            steps
                nodejs('install nodejs') {
                sh 'npm install'
                }
            }
    
        stage('Snyk') {
            steps {
                echo 'Snyk...'
                snykSecurity(
                snykInstallation: 'Snyk-Scan',
                snykTokenId: 'Snyk-Scan',
                )
            }
    }   
        stage('DEV') {
            steps {
                echo 'Building...'
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