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
        }
    }