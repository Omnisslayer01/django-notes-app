@Library('Shared_Library') _

pipeline{
    agent {label 'my_agent'}
    stages{
        stage("Welcome"){
            steps{
              script{
                    hello()
                } 
            }
        }
        stage("Code"){
            steps{
                script{
                    code_clone("https://github.com/LondheShubham153/django-notes-app.git","main")
                }
                // echo "This is cloning the project"
                // git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
                // echo "Code cloned successfully"
                
                echo "Creating dockerignore"
                sh "echo 'data/mysql/' > .dockerignore"
            }
        }
        stage("Build"){
            steps{
                // echo "Stopping old builds if present"
                // sh "docker stop notesapp || true"
                // sh "docker rm notesapp || true"
                
                script{
                    build("temp01011","notesapp","latest")
                }
                // echo "This is building the project"
                // sh "docker build -t notesapp:latest ."
                // sh "docker run -d -p 8000:8000 --name notesapp notesapp"
            }
        }
        stage("Test"){
            steps{
                echo "This is testing the project"
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    docker_push("temp01011","notesapp","latest")
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the project"
                script{
                    deploy_w_compose()
                }
                // sh "docker compose up -d"
            }
        }
    
    }
}
