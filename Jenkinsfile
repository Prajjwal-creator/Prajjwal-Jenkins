pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use 'bat' for Windows instead of 'sh'
                bat 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running unit tests...'
                // Run unit tests (use 'bat' for Windows)
                bat 'mvn test'
            }
            post {
                success {
                    emailext(
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Tests Passed',
                        body: 'All tests passed successfully.'
                    )
                }
                failure {
                    emailext(
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Tests Failed',
                        body: 'Tests failed. Please check the logs.'
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code quality analysis...'
                // Example SonarQube analysis (use 'bat' for Windows)
                bat 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example security scan (use 'bat' for Windows)
                bat 'dependency-check --scan .'
            }
            post {
                success {
                    emailext(
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Security Scan Passed',
                        body: 'Security scan completed successfully.'
                    )
                }
                failure {
                    emailext(
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Security Scan Failed',
                        body: 'Security scan failed. Please check the logs.'
                    )
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Example deployment command for Windows (adjust based on your environment)
                bat 'scp target/myapp.jar user@server:/path/to/deploy/'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
