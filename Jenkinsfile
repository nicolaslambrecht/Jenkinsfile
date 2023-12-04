#!/usr/bin/env groovy

pipeline {

    agent any

    // environment {
    //     // Define your GitHub credentials
    //     // CREDENTIALS = credentials('jenkins')
    //     GIT_SSH_COMMAND = "ssh -i /var/lib/jenkins/.ssh/id_rsa"
    // }

    stages {

        stage('Checkout') {
            steps {
                script {
                    // git branch: 'main', url: 'https://github.com/HoGentTIN/p3ops-demo-app.git'
                    // sh "echo $USER"
                    // sh "pwd"
                    // git branch: 'main', credentialsId: 'jenkins', url: 'git@github.com:HOGENTDevOpsPrj/devops-23-24-net-g11.git'
                    sshagent(credentials: ['jenkins']) {
                        // Use the git step to perform the checkout
                        git branch: 'main', url: 'git@github.com:HOGENTDevOpsPrj/devops-23-24-net-g11.git'
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

            stage('Publish') {
                steps {
                    script {
                        // Publish the .NET project
                        sh 'dotnet publish -c Release -o ./publish'
                    }
                }
            }

        // stage("deploy") {
            
        //     steps {
        //         script {
        //             // sh 'scp -r . operationsg11@104.45.53.118:/home/operationsg11/test'
        //             // Define your application server details
        //             def server = '104.45.53.118'
        //             def remoteDir = '/home/operationsg11/'
        //             def privateKey = """ """
        
        //             // Write the private key to a temporary file
        //             def privateKeyFile = writeFile file: 'private-key.pem', text: privateKey

        //             // Set permissions for the temporary directory
        //             sh "chmod -R 700 private-key.pem"
        
        //             // Copy files to the application server using SCP
        //             sh "scp -i private-key.pem -o StrictHostKeyChecking=no -r ./publish/* ${server}:${remoteDir}"
        
        //             // Clean up the temporary private key file
        //             sh "rm private-key.pem"
        //         }
        //     }
        // }
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
