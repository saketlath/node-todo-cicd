pipeline {
    agent { label "dev-server-agent"}
     
    stages{
        
        stage("Code"){
            steps{
                git url: "https://github.com/saketlath/node-todo-cicd.git", branch: "master"
                echo 'bhaiya code clone ho gya'
            }
        }
        
        stage("Build and Test"){
            steps{
                sh "docker build -t node-app-todo ."
                echo 'bhaiya code build aur test ho gya'
            }
        }
        
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){  
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-todo:latest ${env.dockerHubUser}/node-app-todo:latest"
                sh "docker push ${env.dockerHubUser}/node-app-todo:latest"
                echo 'bhaiya image dockerhun pe push ho gya'
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'bhaiya finally deploy bhi ho gya '
            }
        }
    }
}
