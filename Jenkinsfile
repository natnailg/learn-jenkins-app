
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
        }
        stage('E2E') {
            agent {
                docker {
                    image 'node: mcr.microsoft.com/playwright:v1.48.1-noble'
                    reuseNode true
                }
            }

            steps {
                sh '''
                   npm install -g serve 
                   serve -s build 
                   npx playwright test 
                '''
            }
        }
    }
}
