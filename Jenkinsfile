pipeline {
    agent any
    stages {
        stage("Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch:"main"
            }
            
        }
        
        stage("Build") {
            steps {
                echo "Building the code"
                sh "docker build -t my-note-app ."
            }
        }
        
        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the code to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",usernameVariable:"dockerHubUser",passwordVariable:"dockerHubPass")]){
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
                
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

