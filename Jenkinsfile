pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean install'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test'
                sh 'mvn verify'
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
                sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan with OWASP Dependency Check...'
                sh 'mvn dependency-check:check'
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
                sh 'scp target/your-app.jar ec2-user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                sh 'ssh ec2-user@staging-server "/path/to/run_tests.sh"'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production Environment...'
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
