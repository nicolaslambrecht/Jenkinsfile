#!/usr/bin/env groovy

pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'jenkins', url: 'git@github.com:HOGENTDevOpsPrj/devops-23-24-net-g11.git'
                }
            }
        }


        stage("build") {
            
            steps {
                echo "building the application..."
                script {
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

            stage('Publish') {
                steps {
                    script {
                        // Publish the .NET project
                        sh 'dotnet publish -c Release -o ./publish'
                    }
                }
            }

        stage("deploy") {
            
            steps {
                script {
                    sh "pwd"
                    sh "scp -o StrictHostKeyChecking=no -i /var/lib/jenkins/AppServ2.pem -r /var/lib/jenkins/workspace/Pipe/publish/* operationsg11@51.124.191.97:/home/operationsg11"
                }
            }
        }
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
