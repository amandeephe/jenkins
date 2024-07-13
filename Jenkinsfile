pipeline {
    environment {
        imagename = "ganeshpoloju/jenkinss"
        dockerImage = ''
        containerName = 'my-container'
        dockerHubCredentials = 'admin'
        dockerImageTag = "${imagename}:${env.BUILD_NUMBER}"
    }

    agent any

    stages {
        stage('Cloning Git') {
            steps {
                git(url: 'https://github.com/GANESH0369/jenkins.git', branch: 'main')
            }
        }

        stage('Building image') {
            steps {
                script {
                    dockerImageTag = "${imagename}:${env.BUILD_NUMBER}"
                    dockerImage = docker.build dockerImageTag
                }
            }
        }

        stage('Running image') {
            steps {
                script {
                    sh "docker run -d --name ${containerName} ${dockerImageTag}"
                    // Perform any additional steps needed while the container is running
                }
            }
        }

        stage('Stop and Remove Container') {
            steps {
                script {
                    sh "docker stop ${containerName} || true"
                    sh "docker rm ${containerName} || true"
                }
            }
        }
    }
    } 
    

