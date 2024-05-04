pipeline {
    agent any 
        stages {
            stage("code") {
                steps {
                    echo "cloning the code"
                    git url:"https://github.com/xxx-holic-01/Jenkins.git" , branch: "main"
                }
            }
            stage("build")
                steps {
                    echo "building the image"
                    sh "docker build -t myimage:${BUILD_NUMBER}"

                }
             stage("pushToDockerHub")
                steps {
                    echo "pushing image to dockerHub"
                    
                }
        }
    
}
