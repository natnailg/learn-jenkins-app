
pipeline {
    agent any

    stages {
        /*
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo BUILDING
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }*/
        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.48.1-noble'
                    reuseNode true
                    //args '-u root:root' // running the container as a root (not advised)
                }
            }

            steps {
                sh '''
                   npm install serve 
                   node_modules/.bin/serve -s build & 
                   sleep 10  
                   npx playwright test 
                '''
            }
        }
    }
}
