pipeline {
    agent any

    tools {nodejs "node"}
    environment {
      SEMGREP_APP_TOKEN = credentials('semgrep-scan')
    }

    stages {
        stage ('install deps') {
            steps {
                 sh 'npm install'
            }
        }

        stage('DEV') {
            steps {
                echo 'Building...'
            }
        }

        stage('Semgrep-Scan') {
            steps {
                sh '''docker pull returntocorp/semgrep && \
                docker run \
                -e SEMGREP_APP_TOKEN=$SEMGREP_APP_TOKEN \
                -v "$(pwd):$(pwd)" --workdir $(pwd) \
                returntocorp/semgrep semgrep ci '''
                sh 'exit 0'
            }
        }
    
        stage('Snyk') {
            steps {
                echo 'Snyk Scanning...'
                snykSecurity(
                snykInstallation: 'Snyk-Scan',
                snykTokenId: 'Snyk-Scan',
                additionalArguments: '--severity-threshold=critical'
                // --detection-depth=3
                )
                sh 'exit 0' 
            }
        }
           
        

        stage('TEST') {
            steps {
                echo 'Testing..'
                steps {
                    
                    sh 'docker pull public.ecr.aws/portswigger/dastardly:latest'
                    cleanWs()
                    sh '''
                    docker run --user $(id -u) -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e BURP_START_URL=https://juice-shop.herokuapp.com/ \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                    '''
                }
            }
        }


        stage('PROD') {
            steps {
                echo 'Deploying....'
            }
        }

    }

    // post {
    //     always {
    //         junit testResults: 'dastardly-report.html', skipPublishingChecks: true
    //     }
    // }
}