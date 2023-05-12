pipeline {
    agent any

    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Topsideboss2/django-notes-app.git', branch: 'main'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t notes-app'
                sh 'docker image list'
            }
        }
        stage('Login'){
            steps{
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
                sh 'docker login -u topsideboss2 -p $PASSWORD'
                }
            }
        }
        stage("Push Image to Docker Hub"){
        steps{
            sh 'docker tag notes-app topsideboss2/notes-app:latest'
            sh 'docker push topsideboss2/notes-app:latest'
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}