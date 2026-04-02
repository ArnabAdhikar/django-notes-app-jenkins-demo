pipeline{
    agent { label "bro" }
    environment {
        DOCKER_BUILDKIT = 1
    }
    stages{
        stage("code"){
            steps{
                echo "clonning"
                git url: "https://github.com/ArnabAdhikar/django-notes-app-jenkins-demo.git", branch:"main"
                echo "successful"
            }
        }
        stage("build"){
            steps{
                echo "building"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("push to dockerhub"){
            steps{
                echo "pushing"
                withCredentials([usernamePassword(
                    credentialsId:"DockerHubCreds",
                    usernameVariable:"DockerHubUser", 
                    passwordVariable:"DockerHubPass")]){
                sh 'docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}'
                sh "docker image tag notes-app:latest ${env.DockerHubUser}/notes-app:latest"
                sh "docker push ${env.DockerHubUser}/notes-app:latest"
                echo "Done..."
                }
            }
        }
        stage("deploy"){
            steps{
                echo "deploying"
                sh "docker compose up -d"
            }
        }
    }
}