pipeline {
    agent any
    environment {
        DIRECTORY_PATH = "CODE/WEEK5/5.1P"
        TESTING_ENVIRONMENT = "WEEK_5_TASK_ENVIRONMENT"
        PRODUCTION_ENVIRONMENT = "RIN"
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from $DIRECTORY_PATH"
                echo "Compiling the code and generating necessary artifacts"
            }
	    post{
                success{
                    mail to: "doanvanngoctuong@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was Successful"
                }
        }
        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Checking the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the application to $TESTING_ENVIRONMENT"
            }
        }
        stage('Approval') {
            steps {
                sleep(time: 10, unit: 'SECONDS')
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the code to $PRODUCTION_ENVIRONMENT"
            }
        }
    }
}
