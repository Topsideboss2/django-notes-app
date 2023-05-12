pipeline {
    agent { label 'node-agent' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Topsideboss2/django-notes-app.git', branch: 'main'
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t notes-app'
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
