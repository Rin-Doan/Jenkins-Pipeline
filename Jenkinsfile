pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo"Building ..."
            }
            post{
                success{
                    mail to: "doanvanngoctuong@gmail.com",
                    subject: "Build Status Email",
                    body: "Build was Successful"
                }
            }
        }
    }
}