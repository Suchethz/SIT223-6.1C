pipeline {
    agent any

    tools {
        // Use the configured Maven 3.9.9 in Jenkins
        maven 'Maven 3.9.9'  // Replace with the actual name in Jenkins if different
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Use 'bat' for Windows instead of 'sh'
                bat 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                bat 'mvn test'
                bat 'mvn verify'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Unit and Integration Tests Status',
                         body: 'The Unit and Integration Tests have completed. Please check the logs in Jenkins.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis with SonarQube...'
                bat 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan with OWASP Dependency Check...'
                bat 'mvn dependency-check:check'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Security Scan Status',
                         body: 'The Security Scan has completed. Please check the logs in Jenkins.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Environment...'
                // Example deployment command, adjust as needed
                bat 'scp target/your-app.jar ec2-user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                bat 'ssh ec2-user@staging-server "/path/to/run_tests.sh"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
                bat 'scp target/your-app.jar ec2-user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
