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

        stage('Unit test') {
            steps {
                withEnv(["HOME=${env.WORKSPACE}"]) {
                    // sh "pip install -r requirements.txt --user"
                    sh 'python3 -m pip install semgrep'
                }
            }

            post {
                cleanup {
                    cleanWs()
                }
            }
        }

        stage('Semgrep-Scan') {
            steps {
                // sh 'chmod +x /.cache/pip'
                // sh 'chown -R user:Admin /.cache/pip'
                // sh 'pip install --user --upgrade pip'
                
                // sh 'pip install --user -r requirements.txt'
                sh 'semgrep ci'
                sh 'semgrep --config=auto'
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