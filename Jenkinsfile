pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    args '-u 1000:1000'
                    volumesFrom 'jenkins'
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
