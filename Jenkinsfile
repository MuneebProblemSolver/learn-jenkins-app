pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
              
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                test -f build/index.html
                npm test 
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
              sh '''
                npm install netlify-cli -g
                node_modules/.bin/netlify --version
              '''
            }
        }
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
