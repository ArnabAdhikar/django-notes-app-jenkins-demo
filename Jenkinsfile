@Library("Shared") _
pipeline{
    agent { label "bro" }
    stages{
        stage("hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("code"){
            steps{
                script{
                    clone("https://github.com/ArnabAdhikar/django-notes-app-jenkins-demo.git","main")
                }
            }
        }
        stage("build"){
            steps{
                script{
                    docker_build("notes-app","latest","arnaba075")
                }
            }
        }
        stage("push to dockerhub"){
            steps{
                echo "pushing"
                script{
                    docker_push("notes-app","latest","arnaba075")
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