pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/PrasanthKumar0/FlaskApp-Deployment-Pipeline-with-Jenkins-and-EC2.git'
            }
        }
        stage('Docker Build') {
            steps {
                sh "docker build . --file Dockerfile --tag docker.io/prasanthk8/python-webapp:latest"
            }
            
        }
        stage('Docker Push') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                    sh "make push"  
                        
                    }
                }
            }
            
        }
        stage('Docker Deploy') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'DockerCred', toolName: 'docker') {
                    sh "docker images"  
                    sh "docker run -d -it -p 5000:5000 --name FlaskApp prasanthk8/python-webapp:latest"
                    }
                }
            }
            
        }
    }
}