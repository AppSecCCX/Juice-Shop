pipeline {
    agent any
    
    // tools {nodejs "node"}

    stages {
        // stage ('install deps') {
        //     steps {
        //         // nodejs('install nodejs') {
        //         // sh 'npm install'
        //         // }

        //          sh 'npm install'
        //     }
        // }
    
        stage('Snyk') {
            steps {
                echo 'Snyk...'
                snykSecurity(
                snykInstallation: 'Snyk-Scan',
                snykTokenId: 'Snyk-Scan',
                additionalArguments: '--all-projects --detection-depth=1'
                )
                sh 'cat /var/jenkins_home/workspace/Juiceshop/*_snyk_report.json'
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