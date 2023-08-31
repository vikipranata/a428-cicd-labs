pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3001:3001'
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
            }
        }
        stage('Manual Approval') { 
            steps {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: "MINUTES") {
                sh './jenkins/scripts/kill.sh'
                }
            }
        }
    }
}
