pipeline {

    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }

    parameters {
        choice(choices:['Hello','Bye'], description: 'Users Choice', name: 'CHOICE')
    }

    stages {
        
        stage('Manual Step') {
            steps('Input') {
                echo "choice: ${CHOICE}"
                echo "choice params.: " + params.CHOICE
                echo "choice env: " + env.CHOICE
            }
        }

        stage('Hello') {
            when { 
                expression { env.CHOICE == 'Hello' }
            }   
            
            steps('Execute')    {
                echo 'Say Hello'
            } 
        }

        stage('Bye') {
            when {
                expression {env.CHOICE == 'Bye'}
            }
            
            steps('Execute'){
                echo 'Say Bye'    
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
        
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep 30
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }

    }
    
}