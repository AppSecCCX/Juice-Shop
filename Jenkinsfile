pipeline {
    agent any
    

    // tools {
    //     nodejs '21.6.1'
    // }

    stages {

        stage('Install packages') {
            steps{
                sh ("docker run --user='Admin' --rm -v `pwd`:/app -w /app node nodejs install")
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