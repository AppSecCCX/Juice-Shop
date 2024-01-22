pipeline {
    agent any

    stages {
        stage('DEV') {
            steps {
                echo 'Building..'
            }
        }
        stage('TEST') {
            steps {
                echo 'Testing..'
                snykSecurity(
                snykInstallation: 'Juiceshop',
                snykTokenId: 'e899eecb-2aa3-422f-915e-a2f4482a548a',
        )
            }
        }
        stage('PROD') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}