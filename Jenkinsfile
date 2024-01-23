pipeline {
    agent any 
    tools {nodejs "node"}

    stages {

        stage('node') {
        steps {
            sh 'npm config ls'
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