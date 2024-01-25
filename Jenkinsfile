pipeline {
    agent any

    tools {nodejs "node"}
    environment {
      SEMGREP_APP_TOKEN = credentials('semgrep-scan')
    }

    stages {
        stage ('install deps') {
            steps {
                // nodejs('install nodejs') {
                // sh 'npm install'
                // }

                 sh 'npm install'
            }
        }

        stage('Semgrep-Scan') {
            steps {
                sh '''docker pull returntocorp/semgrep && \
                docker run \
                -e SEMGREP_APP_TOKEN=$SEMGREP_APP_TOKEN \
                -v "$(pwd):$(pwd)" --workdir $(pwd) \
                returntocorp/semgrep semgrep ci '''
            }
        }
    
        stage('Snyk') {
            steps {
                echo 'Snyk Scanning...'
                snykSecurity(
                snykInstallation: 'Snyk-Scan',
                snykTokenId: 'Snyk-Scan',
                // additionalArguments: '--all-projects --detection-depth=3'
                )
                sh 'cd  /var/jenkins_home/workspace/Juiceshop/'
                sh 'cat *_snyk_report.json'
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