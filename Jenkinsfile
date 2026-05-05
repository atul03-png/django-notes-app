pipeline {
    agent any
 
    stages {
 
        stage('code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/atul03-png/django-notes-app'
            }
        }
 
        stage('build') {
            steps {
                sh 'docker build -t notes-app:latest .'
            }
        }
 
        stage('push to docker hub') {
            steps {
                echo "pushing the image to docker hub"
 
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCREd",
                    usernameVariable: "dockerHubUser",
                    passwordVariable: "dockerHubPass"
                )]) {
 
                    sh "docker login -u $dockerHubUser -p $dockerHubPass"
 
                    sh "docker tag notes-app:latest $dockerHubUser/notes-app:latest"
 
                    sh "docker push $dockerHubUser/notes-app:latest"
                }
            }
        }
 
        stage('deploy') {
            steps {
                sh "docker compose up -d"
            }
        }
    }
 
    post {
        always {
            echo "Pipeline finished"
