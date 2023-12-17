pipeline {
        agent any
        stages {

            stage('Checkout') {
                steps {
                    checkout scm
                }
            }

            stage('NPM Install') {
                steps {
                    bat "npm install"
                }
            }

            stage('Run intigration tests') {
                steps {
                    bat "npm run test"
                }
            }

            stage('Build') {
                steps {
                    withCredentials([usernamePassword(credentialsId: '44620164-ae1d-40e8-9be0-a2024ac01d2a', passwordVariable: 'pass', usernameVariable: 'user')]) {
                        bat """docker build -t igotto1/student:1.0.0 .
                            docker login -u %user% --password %pass%
                            docker push igotto1/student: 1.0.0"""
                    }
                }
            }

            stage('Deploy') {
                steps {
                    withCredentials([usernamePassword(credentialsId: '44620164-ae1d-40e8-9be0-a2024ac01d2a', passwordVariable: 'pass', usernameVariable: 'user')]) {
                        bat """docker pull igotto1/student:1.0.0
                            docker run -d -p 8081:8081 igotto1/student:1.0.0"""
                    }
                }
            }
        }
    }