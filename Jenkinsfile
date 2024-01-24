pipeline {
    agent any
    

    // tools {
    //     nodejs '21.6.1'
    // }

    stages {
        
        
        stage('Snyk') {
            steps {
                echo 'Snyk...'
                snykSecurity(
                snykInstallation: 'Juiceshop',
                snykTokenId: 'Juiceshop',
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