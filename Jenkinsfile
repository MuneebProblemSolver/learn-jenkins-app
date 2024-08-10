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
                sh 'apk add --no-cache coreutils'
                sh 'npm install'
                sh 'npm run build'
            }
        }
    }
}
