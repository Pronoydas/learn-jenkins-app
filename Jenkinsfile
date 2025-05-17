pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
               node --version 
               npm --version
               ls -la
               npm ci 
               nmp run build 
               ls -la

               '''
            }
        }
    }
}
