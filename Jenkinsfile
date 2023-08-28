def sendEmailNotification(stageName, successCheck) {
    def buildStatus = successCheck ? 'SUCCESS' : 'FAILURE'
    
    emailext (
        subject: "JENKINS NOTIFICATION",
        body: "Stage ${stageName} ${buildStatus}",
        to: 'doanvanngoctuong@gmail.com', // Update with the appropriate email address
        attachLog: true
    )
}

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Use a build automation tool (e.g., Maven) to build the code
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    // Run unit tests and integration tests using test automation tools
                    sh 'mvn test'
                }
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
                script {
                    // Integrate a code analysis tool (e.g., SonarQube) to analyze the code
                    sh 'mvn sonar:sonar'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                script {
                    // Perform a security scan using a security scanning tool (e.g., OWASP ZAP)
                    sh 'owasp-zap scan -t http://your-app-url'
                }
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
                script {
                    // Deploy the application to a staging server (e.g., AWS EC2 instance)
                    sh 'ssh user@staging-server "bash deploy-script.sh"'
                }
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                script {
                    // Run integration tests on the staging environment
                    sh 'mvn integration-test'
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy the application to a production server (e.g., AWS EC2 instance)
                    sh 'ssh user@production-server "bash deploy-script.sh"'
                }
            }
        }
    }
}
