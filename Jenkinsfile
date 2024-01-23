pipeline {
    agent any
    

    // tools {
    //     nodejs '21.6.1'
    // }

    stages {

        stage('Install packages') {
            steps
                
            }
        }
        
    }   
        stage('DEV') {
            steps {
                echo 'Building...'
                nodejs('install nodejs') {
                sh 'npm install'
                }
            }
        }

        stage('Snyk') {
            steps {
                echo 'Snyk...'
                snykSecurity(
                snykInstallation: 'Juiceshop',
                snykTokenId: 'Juiceshop',
                )
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