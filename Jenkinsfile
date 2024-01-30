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
                // additionalArguments: '--all-projects'
                // --detection-depth=3
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
                steps {
                    sh 'docker pull public.ecr.aws/portswigger/dastardly:latest'
                }
            }
        }
                

         stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                cleanWs()
                sh '''
                    docker run --user $(id -u) -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e BURP_START_URL=https://juice-shop.herokuapp.com/ \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.html \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }



        stage('PROD') {
            steps {
                echo 'Deploying....'
            }
        }

    }

    post {
        always {
            junit testResults: 'dastardly-report.html', skipPublishingChecks: true
        }
    }
}