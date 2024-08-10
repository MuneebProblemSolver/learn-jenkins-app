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
            
            steps {
           echo 'Test Stage'
            }
        }

    }
}
