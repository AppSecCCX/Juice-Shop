pipeline {
    // agent any 
    tools {nodejs "node"}

    stages {

        stage('NODEJS') {
            steps {
                sh 'npm i'
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