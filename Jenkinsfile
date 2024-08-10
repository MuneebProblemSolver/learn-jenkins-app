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

        stage('Test Stage') {
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
    }
    post{
        always{
            junit 'tests-results/junit.xml'
        }
    }
}
