pipeline {
    agent any

    tools {nodejs "node"}
    environment {
      SEMGREP_APP_TOKEN = credentials('semgrep-scan')
      SNYK_TOKEN = credentials('Snyk-Scan')
      DOJO_HOST = 'http://localhost:9000'
      DOJO_API_TOKEN = 'd56d4b30c4b8e877dc0a53fcd46994973f547e68'
    }

    stages {

        stage('DEV') {
            steps {
                echo 'Building...'
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
                sh 'exit 0'
            }
        }
    
        // stage('Snyk') {
        //     steps {
        //         echo 'Snyk Scanning...'
        //         snykSecurity(
        //         snykInstallation: 'Snyk-Scan',
        //         snykTokenId: 'Snyk-Scan',
        //         // additionalArguments: '--detection-depth=3 --all-projects'
        //         )
        //         sh 'exit 0' 
        //     }
        // }

          stage('Download Snyk CLI') {
            //Downloads the latest Snyk CLI tool and authenticates using the Snyk token
            steps {
                script {
                    def latestVersionCLI = sh(
                        script: 'curl -Is "https://github.com/snyk/snyk/releases/latest" | grep "^location" | sed s#.*tag/##g | tr -d "\r"',
                        returnStdout: true
                    ).trim()

                    echo "Latest Snyk CLI Version: ${latestVersionCLI}"

                    def snykCLIDownloadURL = "https://github.com/snyk/snyk/releases/download/${latestVersionCLI}/snyk-linux"
                    echo "Download URL: ${snykCLIDownloadURL}"

                    sh """
                        curl -Lo ./snyk "${snykCLIDownloadURL}"
                        chmod +x snyk
                        ./snyk -v
                        ./snyk auth \${SNYK_TOKEN}
                    """
                }
            }
        }

        stage('Download Snyk Delta') {
            //Downloads the latest Snyk Delta tool required to compare the current scan against an initial profile 
            steps {
                script {
                    def latestVersionDelta = sh(
                        script: 'curl -Is "https://github.com/snyk-tech-services/snyk-delta/releases/latest" | grep "^location" | sed s#.*tag/##g | tr -d "\r"',
                        returnStdout: true
                    ).trim()

                    echo "Latest Snyk Delta Version: ${latestVersionDelta}"

                    def snykDeltaDownloadURL = "https://github.com/snyk-tech-services/snyk-delta/releases/download/${latestVersionDelta}/snyk-delta-linux"
                    echo "Download URL: ${snykDeltaDownloadURL}"

                    sh """
                        curl -Lo ./snykdelta "${snykDeltaDownloadURL}"
                        chmod +x snykdelta
                        ./snykdelta -v
                    """
                }
            }
        }

       
         stage('Snyk Test using Snyk CLI') {
            // conducts a Snyk test scan and compares the results against the defined baseline (initial scan). If no baseline is available this step will fail
            steps {
                sh '''
                    ./snyk test --json --print-deps | ./snykdelta --baselineOrg xxx --baselineProject xxx --setPassIfNoBaseline false 
                '''
            }
         }

         stage('Snyk Monitor using Snyk CLI') {
            // runs a snyk monitor scan if there is no baseline scan
            steps {
                sh './snyk monitor --org xxx'
            }
        }


        stage('Dastadrly Scan...') {
            steps {
                echo 'Dastardly Scanning..'
                steps {
                    
                    sh 'docker pull public.ecr.aws/portswigger/dastardly:latest'
                    cleanWs()
                    sh '''
                    docker run --user $(id -u) -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e BURP_START_URL=https://juice-shop.herokuapp.com \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                    '''
                }
                echo 'Dastardly Scanning Completed.'
                echo 'Upload Dastardly Scan to DefectDojo'
                steps {
                    sh '''
                    upload-results.py --host $DOJO_HOST --api_key $DOJO_API_TOKEN \
                    --engagement_id 1 --product_id 1 --lead_id 1 --environment "Production" \
                    --result_file dastardly-report.xml --scanner "Snyk Scan"
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