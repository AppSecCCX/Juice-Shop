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