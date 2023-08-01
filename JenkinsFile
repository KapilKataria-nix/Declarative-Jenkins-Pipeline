pipeline{
    agent any
    stages{
        stage("Stage-1 Code"){
            steps{
                echo "Clone the code"
                git url: "https://github.com/KapilKataria-nix/UtilMax", branch: "main"
            }
            
        }
        stage("Stage-2 Build"){
            steps{
                echo "Build the code"
                sh "docker build -t util-jenkin-max ."
            }
        }
        stage("Stage-3 Push to DockerHub"){
            steps{
                echo "Push the code to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag util-jenkin-max ${env.dockerHubUser}/util-jenkin-max:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/util-jenkin-max:latest"
                }            
                    
            }
        }
        stage("Stage-4 Deploy"){
            steps{
                echo "Deploy the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
