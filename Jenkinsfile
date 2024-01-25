pipeline {
    // agent any

    agent {
        docker { image 'python:3' }
    }

    // tools {nodejs "node"}
    environment {
      SEMGREP_APP_TOKEN = credentials('semgrep-scan')
    }

    stages {
        // stage ('install deps') {
        //     steps {
        //         // nodejs('install nodejs') {
        //         // sh 'npm install'
        //         // }

        //          sh 'npm install'
        //     }
        // }

        stage('Semgrep-Scan') {
            steps {
                sh 'pip3 install semgrep'
                sh 'semgrep ci'
            }
        }
    
        stage('Snyk') {
            steps {
                echo 'Snyk...'
                snykSecurity(
                snykInstallation: 'Snyk-Scan',
                snykTokenId: 'Snyk-Scan',
                additionalArguments: '--all-projects --detection-depth=1'
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