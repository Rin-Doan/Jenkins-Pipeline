pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Use a build automation tool (e.g., Maven) to build the code
                echo"DESCRIPTION: Build the code using a build automation tool to compile and package your code"
                echo"TOOL: Using Maven as a build automation tool"
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo"DESCRIPTION: run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected "
                echo"TOOL: Using JUnit as a test automation tool"

            }
            post {
                success {
                    emailext to: "doanvanngoctuong@gmail.com",
                    subject: "Unit and Integration Tests",
                    body: "test was successful !!"
                    attachLog:true
                }
                failure {
                    emailext to: "doanvanngoctuong@gmail.com",
                    subject: "Unit and Integration Tests",
                    body: "test was failure !!"
                    attachLog:true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo"DESCRIPTION: integrate a code analysis tool to analyse the code and ensure it meets industry standards."
                echo"TOOL: Using  SonarQube as a code analysis tool"
            }
        }
        
        stage('Security Scan') {
            steps {
                echo"DESCRIPTION:  perform a security scan on the code using a tool to identify any vulnerabilities."
                echo"TOOL: Using   OWASP Dependency-Check as a security scan tool"
            }
            post {
                success {
                    emailext to: "doanvanngoctuong@gmail.com",
                    subject: "Security Scan",
                    body: "scan was successful !!"
                    attachLog:true
                }
                failure {
                    emailext to: "doanvanngoctuong@gmail.com",
                    subject: "Security Scan",
                    body: "scan was failure !!"
                    attachLog:true
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo"DESCRIPTION: deploy the application to a staging server"
                echo"TOOL: Using  AWS EC2 as a deploy to staging tool"
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo"DESCRIPTION: run integration tests on the staging environment to ensure the application functions as expected in a production-like environment."
                echo"TOOL: Using  Citrus to run tests"
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo"DESCRIPTION: - deploy the application to a production server"
                echo"TOOL: Using  AWS EC2 to deploy to production"
            }
        }
    }
}
