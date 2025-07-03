@Library("Shared") _
pipeline{
    agent {label "agent2"}
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/venkyscafe/django-notes-app.git","main")
                }
                //echo "this is cloning the code from git repo"
                //git url:"https://github.com/venkyscafe/django-notes-app.git", branch:"main"
                //echo "code cloning successfull"
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build(
                        imageName: "v3nkys/new-notes-app",
                        imageTag: "latest",
                        dockerfile: "Dockerfile",
                        context: ".")
                }
                //echo "this is building the code"
                //sh "docker build -t my-notes-app:latest ."
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    docker_push(        
                        imageName: "v3nkys/new-notes-app",
                        imageTag: "latest")
                }
                //echo "this is pushing the image to Docker Hub"
                //withCredentials([usernamePassword('credentialsId':"dockerHubCred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
                //{
                //sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                //sh "docker image tag my-notes-app:latest ${env.dockerHubUser}/my-notes-app:latest"
                //sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                //}
            }
        }
        stage("Deploy"){
            steps{
                echo "this is deploying the code"
                //sh "docker run -d -p 8000:8000 my-notes-app:latest"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}