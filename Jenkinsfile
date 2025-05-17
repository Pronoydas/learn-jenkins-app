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
<<<<<<< HEAD
=======

>>>>>>> 410b1b70c036ce61b3362cc5c6367f13725f60cd
               '''
            }
        }
    }
}
