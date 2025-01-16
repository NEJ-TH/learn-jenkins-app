

pipeline 
{
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:20.11.0'
                    reuseNode true
                }               
            }           
            steps {
                sh '''
                node --version
                npm --version                
                export NPM_CONFIG_CACHE=/tmp/npm-cache
                npm ci 
                npm run build
                ls -la
                '''
            }
        }
        stage ('tests')
        {
            agent {
                docker {
                    image 'node:20.11.0'
                    reuseNode true
                }               
            }     
            steps 
            {
            sh '''
            test -f build/index.html
            npm test
            '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'node:20.11.0'
                    reuseNode true
                }               
            }           
            steps {
                sh '''
                npm install netlify-cli -
                node_modules/.bin/netlify --version               
                '''
            }
        }
    }
    post {
        always {
            junit 'tests-result/Junit.xml'
        }
    }
    
}
