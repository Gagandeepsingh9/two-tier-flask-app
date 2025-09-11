@Library("shared") _
pipeline{
    agent any
    stages{
        stage("cloning code"){
            steps{
                script{
                    clone("https://github.com/Gagandeepsingh9/two-tier-flask-app","master")
                }
            }
        }
        stage("checking vulnerbilities"){
            steps{
                script{
                    trivy()
                }
            }
        }
        stage("building image"){
            steps{
                script{
                docker_build("myflaskapp:latest")
                }
            }
        }
        stage("push to dockerhub"){
            steps{
                script{
                    docker_push("DockerHubCreds","myflaskapp:latest")
                }
            }
        }
        stage("deploy"){
            steps{
                script{
                docker_deploy()
                }
            }
        }
        }
    post{
        success{
            emailext(
                to: "gagan13.ca@gmail.com",
                subject: "This is From Jenkins",
                body: "Congratulations! The Build is Successfully Deployed"
            )
        }
        failure{
            emailext(
                to: "gagan13.ca@gmail.com",
                subject: "This is From Jenkins",
                body: "Sorry! Build Failed"
            )
        }
    }
}
