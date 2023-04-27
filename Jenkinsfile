pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('vitaliimakushko-dockerhub')
    }
    stages {
        stage('Docker version') {
            steps {
                sh '''
                    echo $USER
                    docker version
                '''
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t vitaliimakushko/html:latest .'
            }
        }
        stage('Login') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push'){
            steps{
                sh 'docker push vitaliimakushko/html:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
  
