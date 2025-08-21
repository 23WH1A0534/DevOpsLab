pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/23WH1A0534/DevOpsLab.git'
            }
        }

        stage('Package') {
            steps {
                bat 'powershell Compress-Archive -Path Registration.html -DestinationPath registration-form.zip -Force'
                archiveArtifacts artifacts: 'registration-form.zip', fingerprint: true
            }
        }
    }
}
