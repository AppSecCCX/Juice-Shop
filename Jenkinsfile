pipeline {
    agent any

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

        stages {
            stage('Semgrep-Scan') {
                steps {
                    sh 'pip3 install semgrep'
                    sh 'semgrep ci'
                }
            }
        }

        stage ('Check secrets') {
            steps {
                sh 'docker run  gesellix/trufflehog --json https://github.com/shubnimkar/CI_CD_Devsecops.git > trufflehog.json'

                script {
                    def jsonReport = readFile('trufflehog.json')
                    
                    def htmlReport = """
                    <html>
                    <head>
                        <title>Trufflehog Scan Report</title>
                    </head>
                    <body>
                        <h1>Trufflehog Scan Report</h1>
                        <pre>${jsonReport}</pre>
                    </body>
                    </html>
                    """
                    
                    writeFile file: 'scanresults/trufflehog-report.html', text: htmlReport
                }
                archiveArtifacts artifacts: 'scanresults/trufflehog-report.html', allowEmptyArchive: true
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