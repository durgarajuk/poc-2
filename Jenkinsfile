pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/durgarajuk/poc-2.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t java-poc:v1 .'
            }
        }
        stage('Test Inside Container') {
            steps {
                // UPDATE THIS LINE TO MATCH YOUR CURRENT Hello.java OUTPUT
                sh '''
                docker run --rm java-poc:v1 sh -c "java Hello | grep 'Hello, this is a live demo!'"
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker rm -f java-poc-container || true
                docker run -d --name java-poc-container java-poc:v1
                '''
            }
        }
    }
}
