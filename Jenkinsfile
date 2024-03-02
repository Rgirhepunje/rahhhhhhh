pipeline {
    agent {
        docker {
            image 'abhishekf5/maven-abhishek-docker-agent:v1'
             args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
               sh 'echo passed'
            //git branch: 'main', url: 'https://github.com/Rgirhepunje/rahhhhhhh.git'
            }
        }
        
        stage('check') {
            steps {
                script {
                    sh 'ls -l'  // List files in the current directory
                    sh 'cat Dockerfile'  // Display the content of the Dockerfile
                    sh 'docker build -t rgirhepu/ultimate-cicd:17 .'
                }
            }
        }
    
        stage('Build and Push Docker Image') {
            environment {
            DOCKER_IMAGE = "rgirhepu/ultimate-cicd:${BUILD_NUMBER}"
            REGISTRY_CREDENTIALS = credentials('Docker_cred')
            }
            steps {
                script {
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                    def dockerImage = docker.image("${DOCKER_IMAGE}")
                    docker.withRegistry('https://index.docker.io/v1/', "Docker_cred") {
                    dockerImage.push()
                }
            }
        }
    }
}
}
    
