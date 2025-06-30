pipeline{
    agent any 


    environment {

        NETLIFY_PROJECT_ID = '72208a0a-930e-49c0-a52a-2ca70690fcdd'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')

    }

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
                node_modules/.bin/netlify --version
                node_modules/.bin/netlify status

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