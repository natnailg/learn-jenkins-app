pipeline {
    agent any
    // environment variable 
    environment {
        NETLIFY_SITE_ID = 'e0730d03-d926-4351-8d12-38aedba0dbf5'
    }

    stages {
        stage('build') {
            agent {
                docker { 
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version 
                    npm ci 
                    npm run build 
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
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

        stage('Deploy') {
            agent {
                docker { 
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                   npm install netlify-cli 
                   node_modules/.bin/netlify --version
                   echo "deploying to production: Site ID: $NETLIFY_SITE_ID"
                '''
            }
        }


    }

    post {
        always{
            junit 'test-results/junit.xml'
        }
    }
}
