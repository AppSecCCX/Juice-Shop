pipeline {
    agent any 
    // tools {
    //     nodejs '21.6.1'
    // }

    stages {

        // stage('node') {
        //     steps {
        //         sh 'npm version'
        //     }
        // }

        stage('Snyk') {
      steps {
        echo 'Testing...'
        snykSecurity(
          snykInstallation: 'Juiceshop',
          snykTokenId: 'e899eecb-2aa3-422f-915e-a2f4482a548a',
          // place other optional parameters here, for example:
          additionalArguments: '--all-projects --detection-depth=<DEPTH>'
        )
      }
    }

        stage('DEV') {
            steps {
                echo 'Building..'
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