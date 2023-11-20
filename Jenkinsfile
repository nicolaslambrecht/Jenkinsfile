#!/usr/bin/env groovy

pipeline {

    agent any

    environment {
        // // Define your GitHub credentials
        // GITHUB_CREDENTIALS = credentials('jenkins')
        // // Define the path to your private key used for accessing GitHub
        // SSH_PRIVATE_KEY = credentials('~/.ssh/id_rsa')
        
        // Define your server credentials
        SERVER_USER = 'operationsg11'
        SERVER_IP = '104.45.53.118'
        SERVER_PORT = 22
        // SERVER_PATH = '/path/to/deploy'
    }

    stages {

        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/HoGentTIN/p3ops-demo-app.git'
                }
            }
        }

        stage("build") {
            
            steps {
                echo "building the application..."
                script {
                    sh "echo $USER"
                    sh 'dotnet restore'
                    sh 'dotnet build'
                }
            }
        }

        stage("test") {
            
            steps {
                echo "testing the application..."
                script {
                    //unit testing
                    sh 'dotnet test'
                }
            }
        }

    //     stage("deploy") {
            
    //         steps {
    //             // nog geen idee hoe dit te doen
    //         }
    //     }
    }

    post {
        success {
            echo 'Build successful!'
        }

        failure {
            echo 'Build failed!'
        }
    }
}
