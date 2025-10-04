pipeline {
    agent any
    tools {
        nodejs "NodeJS"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Bhautik2902/portfolio-json.git'
            }
        }
	stage('Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-json .'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker stop portfolio-json || true
                docker rm portfolio-json || true
                docker run -d --name portfolio-json -p 5000:5000 portfolio-json
                '''
            }
        }
    }
    triggers {
        githubPush()
    }
}
