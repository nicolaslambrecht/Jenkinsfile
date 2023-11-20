#!/usr/bin/env groovy

pipeline {

    agent any

    // environment {
    //     // Define your GitHub credentials
    //     GITHUB_CREDENTIALS = credentials('jenkins')
    //     // Define the path to your private key used for accessing GitHub
    //     SSH_PRIVATE_KEY = credentials('~/.ssh/id_rsa')
    // }

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
