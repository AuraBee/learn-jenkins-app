pipeline {
    agent any

    stages {
        stage('Build'){
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
        stage('Test'){
             agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    }
                }
            
            steps {
                sh '''
                    echo "Test stage"
                    test -f build/index.html
                    npm test

                '''
            }
        }

        stage('E2E'){
             agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.48.1-noble'
                    reuseNode true
                    }
                }
            
            steps {
                sh '''
                    npm install serve
                    node_modules/serve -s build 
                    npx playwright test
                '''
            }
        }
    }

    
    post {
        always {
            junit 'test-results/junit.xml'
            }
    }
}