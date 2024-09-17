pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Stage 1: Build Process'
                echo 'Details: The code is being built using an automation tool that compiles and packages the application.'
                echo 'Automation Tool: Maven is being utilized for automating the build process.'
                // Example build command (replace with your actual build command)
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Testing'
                echo 'Details: Executing unit tests to verify functionality and integration tests to ensure that all components work together as intended.'
                echo 'Testing Framework: JUnit 5 is used for performing unit tests.'
                // Example test command
                sh 'mvn test'
            }
            post {
                success {
                    emailext(
                        attachLog: true,
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Unit and Integration Tests: Success',
                        body: 'Stage 2 has successfully passed. Please refer to the attached logs for more information.'
                    )
                }
                failure {
                    emailext(
                        attachLog: true,
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Unit and Integration Tests: Failure',
                        body: 'Stage 2 failed. Please check the attached logs for further details.'
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Quality Analysis'
                echo 'Details: Performing a code analysis to ensure it adheres to industry standards and best practices.'
                echo 'Analysis Tool: SonarQube is employed for static code analysis.'
                // Example SonarQube command
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Vulnerability Scan'
                echo 'Details: Conducting a security scan to identify potential vulnerabilities in the application.'
                echo 'Security Tool: OWASP Dependency-Check is utilized for scanning vulnerabilities.'
                // Example security scan command
                sh 'dependency-check --scan .'
            }
            post {
                success {
                    emailext (
                        attachLog: true,
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Security Scan: Successful',
                        body: 'Stage 4 completed successfully. Logs are attached for reference.'
                    )
                }
                failure {
                    emailext(
                        attachLog: true,
                        to: 'prajjwalmakkar0405@gmail.com',
                        subject: 'Security Scan: Failed',
                        body: 'Stage 4 encountered a failure. Logs are attached for review.'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deployment to Staging'
                echo 'Details: Deploying the application to the staging environment, simulating a production-like AWS EC2 instance.'
                // Example deployment command to staging
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy/'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Testing in Staging'
                echo 'Details: Running integration tests in the staging environment to ensure the application behaves as expected in a production-simulated environment.'
                // Example integration test command on staging
                sh './run-integration-tests.sh'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deployment to Production'
                echo 'Details: Deploying the application to the production environment on AWS EC2.'
                // Example deployment command to production
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy/'
            }
        }
    }
}
