pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = 'ade1f28b-ba5b-44f1-8a34-113708775359'
        NETLIFY_AUTH_TOKEN = credentials('Netlify-token')
    }

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
                rm -rf node_modules
                npm install netlify-cli 
                node_modules/.bin/netlify --version
                echo 'Deploy to the Production to site | Site ID : $NETLIFY_SITE_ID'
                node_modules/.bin/netlify status
                node_modules/.bin/netlify deploy --dir=build --prod
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
