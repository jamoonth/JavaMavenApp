pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/jamoonth/JavaMavenApp.git',
                    credentialsId: 'github'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def appVersion = '1.0'
                    sh "docker build -t jamoonth/java-maven-app:${appVersion} ."
                    sh "docker tag jamoonth/java-maven-app:${appVersion} jamoonth/java-maven-app:latest"
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    sh 'docker push jamoonth/java-maven-app:1.0'
                    sh 'docker push jamoonth/java-maven-app:latest'
                }
            }
        }
    }
}
