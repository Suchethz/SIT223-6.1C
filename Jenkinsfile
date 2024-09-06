pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Example: Specify a tool like Maven for building
                echo 'Using Maven for build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Example: Specify JUnit for Unit tests
                echo 'Using JUnit for unit tests'
                // Example: Specify a tool like TestNG for integration tests
                echo 'Using TestNG for integration tests'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Unit and Integration Tests Status',
                         body: 'Unit and Integration Tests have completed. Please check the Jenkins console for details.'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing Code Analysis...'
                // Example: Specify SonarQube for code analysis
                echo 'Using SonarQube for code analysis'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Example: Specify OWASP Dependency Check for security scan
                echo 'Using OWASP Dependency Check for security scanning'
            }
            post {
                always {
                    mail to: 'abhimani.gamage1@gmail.com',
                         subject: 'Security Scan Status',
                         body: 'Security Scan has completed. Please check the Jenkins console for details.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging Environment...'
                // Example: Deploy to AWS EC2 or any other staging server
                echo 'Deploying to staging server using AWS EC2'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example: Run integration tests in the staging environment
                echo 'Running integration tests on staging server'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
                // Example: Deploy to AWS EC2 or another production server
                echo 'Deploying to production server using AWS EC2'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
