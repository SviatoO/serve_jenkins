pipeline {
    agent any

    stages {
        stage('Clone Dockerfile') {
            steps {
                git clone https://github.com/SviatoO/serve_jenkins.git
            }
        }
        stage('Build') {
            steps {
                docker build -t sviato/visdom .
            }
        }
    }
}