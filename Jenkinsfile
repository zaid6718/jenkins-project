pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker_login')
    }

    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/zaid6718/for_project_purpose.git'
            }
        }
        stage('build') {
            steps {
                script{
                    sh 'docker image build -t zaid_website_2.0 .'
                }
            }
        }
        stage('Depploy to port') {
            steps {
                sh 'docker container run -d -p 8000:80 -t zaid_website_2.0'
            }
        }
        stage('Docker logging') {
            steps {
                script{
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        stage('Docker push') {
            steps {
                script{
                    sh 'docker image tag zaid_website_2.0 zaid6718/zaid_website_2.0'
                    sh 'docker push zaid6718/zaid_website_2.0'
                }
            }
        }
        
    }
}
