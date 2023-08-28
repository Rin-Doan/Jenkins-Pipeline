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
                sh 'mvn clean install'
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
                // Perform a security scan on the code using a tool such as OWASP Dependency-Check to identify any vulnerabilities
                sh 'mvn org.owasp:dependency-check-maven:check'
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
                // Deploy the application to a staging server such as an AWS EC2 instance
                sh 'scp target/my-app.war ec2-user@staging-server:/var/lib/tomcat8/webapps/'
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
                // Deploy the application to a production server such as an AWS EC2 instance
                sh 'scp target/my-app.war ec2-user@production-server:/var/lib/tomcat8/webapps/'
            }
        }
    }
}
