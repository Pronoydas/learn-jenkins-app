pipeline{
    agent any 

    stages{

        stage("Build"){

            agent {
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps{
               sh '''
               ls -la 
               node --version
               npm --version
               npm ci 
               npm run build


               '''
            }
        }

        stage("Test"){

            agent{
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps{
                sh '''
                test -f build/index.html
                npm test

                '''
            }

        }

        stage("End To End"){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.53.0-noble'
                    reuseNode true
                }
            }
            steps{
                
                sh '''

                npm install serve
                node_modules/.bin/serve -s build &
                sleep 30

                '''

            }
        }

        stage("Deploy"){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true 
                }
            }
            steps{
                sh '''
                
                npm install  netlify-cli
                netlify --version

                '''

            }
        }

    }

    post{
        always{
            junit 'jest-results/junit.xml'
        }
    }
}