pipeline {

    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
                input(message: 'Please validate, this job will automatically ABORTED after 30 minutes even if no user input provided', ok: 'Proceed')
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep 3
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    
}