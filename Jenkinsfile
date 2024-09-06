pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Using Maven to build the project
                sh 'mvn clean install'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Running unit tests with JUnit
                sh 'mvn test'
                // Running integration tests
                sh 'mvn verify'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Unit and Integration Tests Status',
                         body: 'The Unit and Integration Tests have completed. Logs attached.',
                         attachLog: true
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis with SonarQube...'
                // Running SonarQube for static code analysis
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan with OWASP Dependency Check...'
                // Running OWASP Dependency Check for security vulnerabilities
                sh 'mvn dependency-check:check'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Security Scan Status',
                         body: 'The Security Scan has completed. Logs attached.',
                         attachLog: true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Environment...'
                // Deploying to a staging server (e.g., AWS EC2)
                sh 'scp target/your-app.jar ec2-user@staging-server:/path/to/deploy'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Running integration tests on the staging environment
                sh 'ssh ec2-user@staging-server "/path/to/run_tests.sh"'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
                // Deploying to the production server (e.g., AWS EC2)
                sh 'scp target/your-app.jar ec2-user@production-server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
