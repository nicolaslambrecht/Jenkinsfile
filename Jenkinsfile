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
                    sh "scp -i /home/vagrant/AppServ_key.pem -r /var/lib/jenkins/workspace/Pipe/publish/* operationsg11@104.45.53.118:/home/operationsg11/DotnetApp"
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
