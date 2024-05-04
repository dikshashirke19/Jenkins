pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/xxx-holic-01/Jenkins.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t test:${BUILD_NUMBER} ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"jenkins_test",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag test:${BUILD_NUMBER} ${env.dockerHubUser}/test:${BUILD_NUMBER}"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/test:${BUILD_NUMBER}"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose -f docker-compose.yaml down && docker-compose -f docker-compose.yaml up -d"
                
            }
        }
    }
}
