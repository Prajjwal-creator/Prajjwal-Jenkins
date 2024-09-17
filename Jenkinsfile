pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example build command (Maven)
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running unit tests...'
                // Run unit tests (JUnit)
                sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        to: 'prajjwalmakkar@gmail.com',
                        subject: 'Tests Passed',
                        body: 'All tests passed successfully.'
                    )
                }
                failure {
                    emailext(
                        to: 'prajjwalmakkar@gmail.com',
                        subject: 'Tests Failed',
                        body: 'Tests failed. Please check the logs.'
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code quality analysis...'
                // Example code analysis (SonarQube)
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Example security scan (OWASP Dependency Check)
                sh 'dependency-check --scan .'
            }
            post {
                success {
                    emailext(
                        to: 'prajjwalmakkar@gmail.com',
                        subject: 'Security Scan Passed',
                        body: 'Security scan completed successfully.'
                    )
                }
                failure {
                    emailext(
                        to: 'prajjwalmakkar@gmail.com',
                        subject: 'Security Scan Failed',
                        body: 'Security scan failed. Please check the logs.'
                    )
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Example deployment command (adjust to your environment)
                sh 'scp target/myapp.jar user@server:/path/to/deploy/'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
