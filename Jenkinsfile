def sendEmailNotification(stageName, successCheck) {
    def buildStatus = successCheck ? 'SUCCESS' : 'FAILURE'
    
    emailext (
        subject: "JENKINS NOTIFICATION",
        body: "Stage ${stageName} ${buildStatus}",
        to: 'doanvanngoctuong@gmail.com',
        attachLog: true
    )
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Use a build automation tool (e.g., Maven) to build the code
                sh 'mvn clean package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                // Run unit tests and integration tests using test automation tools
                sh 'mvn test'
            }
            post {
                success {
                    sendEmailNotification("Unit and Integration Tests", true)
                }
                failure {
                    sendEmailNotification("Unit and Integration Tests", false)
                }
            }
        }

        stage('Code Analysis') {
            steps {
                // Integrate a code analysis tool (e.g., SonarQube) to analyze the code
                // This step requires proper setup of the code analysis tool and its configuration
                sh 'mvn sonar:sonar'
            }
        }
        
        stage('Security Scan') {
            steps {
                // Perform a security scan using a security scanning tool (e.g., OWASP ZAP)
                // This step requires proper setup of the security scanning tool
                sh 'owasp-zap scan -t http://your-app-url'
            }
            post {
                success {
                    sendEmailNotification("Security Scan", true)
                }
                failure {
                    sendEmailNotification("Security Scan", false)
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                // Deploy the application to a staging server (e.g., AWS EC2 instance)
                // This step requires proper deployment configuration
                sh 'ssh user@staging-server "bash deploy-script.sh"'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                // Run integration tests on the staging environment
                // This might involve sending API requests or running tests against the deployed app
                sh 'mvn integration-test'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                // Deploy the application to a production server (e.g., AWS EC2 instance)
                // This step requires proper deployment configuration
                sh 'ssh user@production-server "bash deploy-script.sh"'
            }
        }
    }
}
