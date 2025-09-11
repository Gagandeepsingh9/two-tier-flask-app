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
                sh "docker build -t myflaskapp:latest ."
            }
        }
        stage("push to dockerhub"){
            steps{
                script{
                    creds("DockerHubCreds","myflaskapp:latest")
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
