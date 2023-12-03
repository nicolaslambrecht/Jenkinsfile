#!/usr/bin/env groovy

pipeline {

    agent any

    // environment {
    //     // Define your GitHub credentials
    //     // GITHUB_CREDENTIALS = credentials('jenkins')
    //     // Define the path to your private key used for accessing GitHub
        
    //     // Define your server credentials
    //     // SERVER_USER = 'operationsg11'
    //     // SERVER_IP = '104.45.53.118'
    //     // SERVER_PORT = 22
    //     // SERVER_PATH = '/path/to/deploy'
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
                    // sh 'scp -r . operationsg11@104.45.53.118:/home/operationsg11/test'
                    // Define your application server details
                    def server = '104.45.53.118'
                    def remoteDir = '/home/operationsg11/'
                    def privateKey = """-----BEGIN RSA PRIVATE KEY-----
                    MIIG4wIBAAKCAYEAp2JC7Br9hOQ/5fdB19VGafqM+2FqMWBwTIhHcHiFOo54mFSL
                    Jgtn32Y3T0ryY9oBB2+xGg36WJArFyWmu8NIGTrGlahuwE4gVfDCw1cLZthNoYHb
                    gMaFXeIqf8wm/bNUPH7VFYruU1xna9GNXWmK+Qi7PsrI/R1cdnoj42r0AEVJHidZ
                    7kaR0nC7MvfC5+xfVEFpqfLWw1FClxbItkxcteh3gPPa8gxgqJISY0uZTX61FsYq
                    H7LhhKABtebIqnGsPWS+Kp3NkMGyVaEjLcri9j2lMdjf2vwwrQREBfcKlU3JE2dY
                    etLs5tI5E5ggMW8yyFy56D5IRfKHyKKBkSyfL4WR0zlCpwPuRsZiWgWjULGgsLla
                    wU9cDlEr2sTygROwGdZGx1avvLciwaHywzxnBXM7998ZJQz+tSIff8sOHu32Ac+h
                    zngtiXElCMZF4sxM6jamMyjH5W375p9aLiXq0mHO4I0KOr2MMEvdcGa+8kFz9uDa
                    tbPLe0OFojinWR+hAgMBAAECggGBAJ9QJhQlaFEZEjxmR1QPmZJ7N753rKRMfvZI
                    634AKAZg3iVWqo5OYtI9rr0Yv3YMY9hZFX6P+UxcA7dnTbf+mVvyFlsRUkBU2/AQ
                    VL+p1J9Rlyn2uB5sVTnTbtHuVNo52h4uNc/oSQgstf7oF53mO7Dl/5o3Vm+bh4r4
                    m7nz7UNorrw1hiIFJvvd8j8DlI4760v9an2oNYL3j+LQe78PFVrKZRvmfejNoR4w
                    0bGSndollGSVvjgngQBDbv1cKHgZ8eSjudMNfzrQW8R0aVTU6hkQYPX+uzjaKEJT
                    7nkx/uXBHbz23AXJzCE9eFzaHLbWH+gDUwovbSUsF+8Xf6BtUt3rT/GfjCjM5TYO
                    floox9ZUsszg0P5UjFUmWnR7WnIjZCbOX9nHRotmo2cgEf5I/8gJUghwjDNPdZX7
                    X5havN1SmufVa41rfVMv1HKQypx8XuC2lFmbFrx6w3RR5RR0lFEz/J6Np3HAw9CC
                    8tBw+V0lpHmH1CeCCdOW8ULkg/yKNQKBwQDX3sOvy1dU2pQTyNciJ3KCnvSj7qJn
                    M/au4lSLdt8pzHU9d+GVBau4pJUmPeU4yErGg5lzsNFjqRfIody3IZFwqSMUZEum
                    M9Puo8+yv512WJY6d/P6E/V1CzPDzFXedESNImGZOOkkvhSZKNKewfD88qwy1Yai
                    ZlzpiqvZvUHaICUtBWWYbFLhUgrPYaTzNZnddMAlyELLHInnEknw7fjYHA/b4QKP
                    IhZWv14hqQUS3ms6u4jBXj/FPTDRnRqUFQsCgcEAxoAJtf5N9qkXRMuFnc/024Iu
                    wd2cZMJ435XLW6cJ9/ikrnr/vtWVBb0ElLkU2lPemq3Nziethe2Aa27jiacZAp9s
                    BUWyT9MJitmv19DliXZkhxNXigm8EDG/+8tzbaTVC0pyTWOMP0/O3r7dmxHeTzgY
                    e0fYTgvWxvAQiliNg1khvcTVKI1LLOiD/zeA7EbZWDm0YDD/VySCkfZoypbGY51Z
                    MaKYPjQ7ds01g8Ip0rewwl3G8JQBGwbqKbQ1KfGDAoHAZ7bIb+qTP9pwcHz7F5a6
                    RpWWVjit4EWwDGADXKo1GAD6hxjU0eNSmLjCTAhK3BgnDO9nR5U5VNeF7MgPohDH
                    rsgkaYSyb9zQwwQDIw862QRA0UCWgJ0cPiquqTDARMu5r9FH8PTN1vBYNynM36ew
                    X+c74oSCVf42P6J3ZHqwa9sr4VCJekz5GPZw6SgxtwQWs7aHJt/rb2h7vQAldFLx
                    TutUl0CpGRm4f98bm7J4FJO2ExbM4pKkst/uV5dSkLj3AoHAHjKIR6mCTs32fj6/
                    +vwR8friBhginKmBHfJ5112YBKNM2kZX9b4kR5UzxzRI2dX8fWeHcZ9TpJY2/SEH
                    eH91LJL4Ke0qbT5bq0XmnFxpLvpV3L6yiItmksgevr16t+llh6wxq1hDk7YecIB0
                    0gxr131fLBIH9AeVCvqmaYWDMcIzgd0Z2Gt2TkSpIABfmpJEqklNCX0quyUQwAfO
                    dVNupuTfFs/3fS8RBMe/JmY5WpcbStZdV2gMqwHoSaPimpjlAoHAX1TKxrrkH2l/
                    C8MOe7j1PUjqHGFgGxkfPQU6Huv1kDX5b4oV0E3/JnNPsUBQF2CrE6jheXDXgsjB
                    ioCz9sMAyqVxE7Twa0z71pa5xhjPmXiEXpfwdrRlztqFsiRC7QF1CpG1ixYKAQae
                    i8l2Cbywox09F9pLHGx23fmSm804aCtBiNtygs2IPBpYYoYzsrdh+eba3k5PkNVe
                    pabiYL1hW0WFTPf0dF8zgVrLPVovlIQeWk3KmTFUvAto+K7+PHO5
                    -----END RSA PRIVATE KEY-----"""
        
                    // Write the private key to a temporary file
                    def privateKeyFile = writeFile file: 'private-key.pem', text: privateKey

                    // Set permissions for the temporary directory
                    sh "chmod -R 777 ${privateKeyFile}"
        
                    // Copy files to the application server using SCP
                    sh "scp -i ${privateKeyFile} -o StrictHostKeyChecking=no -r ./publish/* ${server}:${remoteDir}"
        
                    // Clean up the temporary private key file
                    sh "rm ${privateKeyFile}"
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
