pipeline {
    agent { 
    node { label 'master' }
     }
     
    environment {
        CI = 'true'	
    }
    stages {
        stage('Build') {
            env.NODEJS_HOME = "${tool node-13.5.0}"
            env.PATH="${env.NODEJS_HOME};${env.PATH}"
            echo ${env.PATH}
            bat 'node -version'
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}		
