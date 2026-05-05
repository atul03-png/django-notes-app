pipeline {
    agent any

    stages {

        stage('code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/atul03-png/django-notes-app.git'
            }
        }

        stage('build') {
            steps {
                sh 'docker build -t notes-app:latest .'
            }
        }

        stage('deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }

    }

    post {
        always {
            echo "Pipeline finished"
        }
    }
}
