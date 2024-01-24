pipeline {
    agent any

    stages {
        stage('Install packages') {
            steps {
//                 script {
//                    docker.image('node:10-stretch').inside { c ->
                        echo 'Building..'
                        sh 'npm install'
                        echo 'Testing..'
                        sh 'npm test'
//                         sh "docker logs ${c.id}"
//                    }
//                 }
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