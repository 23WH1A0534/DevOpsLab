pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate HTML') {
            steps {
                echo "Skipping HTML validation (tidy not available on Windows)"
            }
        }

        stage('Package') {
            steps {
                // Use PowerShell to create a zip instead of Linux zip
                bat 'powershell Compress-Archive -Path index.html -DestinationPath registration-form.zip -Force'
                
                // Save zip file as Jenkins artifact
                archiveArtifacts artifacts: 'registration-form.zip', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying registration form to web server..."
                
                // Example: if using XAMPP on Windows
                bat 'copy index.html C:\\xampp\\htdocs\\index.html /Y'
            }
        }
    }

    post {
        success {
            echo 'Registration form pipeline completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
