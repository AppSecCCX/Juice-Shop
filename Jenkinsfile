pipeline {
    agent any

    stages {
        stage('Install packages') {
            steps
                nodejs('install nodejs') {
                sh 'npm prune'
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