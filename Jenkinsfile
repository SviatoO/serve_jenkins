pipeline {
    environment {
        docker_registry = "sviato/visdom_server"
        docker_registry_credential = credentials('docker_hub_password')
    }
    agent any
    stages {
        stage('Clonning Dockerfile') {
            steps {
                sh "git clone https://github.com/SviatoO/serve_jenkins.git"
            }
        }
        stage('Build docker image') {
            steps {
                sh "cd serve_jenkins && docker build -t $docker_registry:$BUILD_NUMBER ."
            }
        }
        stage('Deploy to DockerHub') {
            steps {
                sh "docker login --username sviato --password $docker_registry_credential"
                sh "docker push $docker_registry:$BUILD_NUMBER"
            }
        }
        stage('Remove unused files and docker image') {
            steps {
                sh "docker rmi $docker_registry:$BUILD_NUMBER"
                sh "cd /home/node/jenkins/workspace/serve_docker_pipeline && rm -rf serve_jenkins"
            }
        }
    }
}