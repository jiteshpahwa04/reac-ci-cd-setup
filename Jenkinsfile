pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {
        stage ('Hello') {
            steps {
                echo 'Hello, World!'
            }
        }

        stage ('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage ('Checkout using SCM') {
            steps {
                checkout scm
            }
        }

        stage ('Build') {
            agent {
                docker {
                    image 'node:22.11.0-alpine3.20'
                    args '-u root'
                    reuseNode true // Reuse the same workspace on the agent
                }
            }

            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -la
                '''
            }
        }

        stage ('Test') {
            agent {
                docker {
                    image 'node:22.11.0-alpine3.20'
                    args '-u root'
                    reuseNode true // Reuse the same workspace on the agent
                }
            }

            steps {
                sh '''
                    ls -la
                    npm test
                '''
            }
        }
    }
}