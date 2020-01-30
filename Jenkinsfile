pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build . -t karthequian/helloworld:latest"
            }
        }
        stage('DockerHub Push'){
            steps{
                    sh "sudo docker tag karthequian/helloworld:latest iad.ocir.io/idreywyoj0pu/helloworld-ng:latest"
                    sh "sudo docker push iad.ocir.io/idreywyoj0pu/helloworld-ng:latest"
            }
        }
        stage('Deploy to k8s'){
            steps{
                sh "sudo /usr/local/bin/kubectl create -f deployment.yml"
                       
            }
        }  
    }
}


def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
