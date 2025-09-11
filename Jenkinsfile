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
        stage("building image"){
            steps{
                sh "docker build -t myflaskapp:latest ."
            }
        }
        stage("push to dockerhub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCreds",
                    usernameVariable: "mydockeruser",
                    passwordVariable: "mydockerpass")]){
                sh "docker login -u ${env.mydockeruser} -p ${env.mydockerpass}"
                sh "docker image tag myflaskapp:latest ${env.mydockeruser}/myflaskapp:latest"
                sh "docker push ${env.mydockeruser}/myflaskapp:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
        }
}
