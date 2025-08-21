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
                // Install tidy on Jenkins machine (Linux: sudo apt install tidy)
                sh 'tidy -errors -q index.html || true'
            }
        }

        stage('Package') {
            steps {
                sh 'zip -r registration-form.zip index.html'
                archiveArtifacts artifacts: 'registration-form.zip', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                // Example: copy file to local Apache web server directory
                sh 'sudo cp index.html /var/www/html/index.html'
            }
        }
    }

    post {
        success {
            echo 'Registration form deployed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
