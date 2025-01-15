

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
                npm cache clean --force
                export NPM_CONFIG_CACHE=/tmp/npm-cache
                npm ci 
                npm run build
                ls -la
                '''
            }
        }
        stage ('tests')
        {
            steps 
            {
            sh '''
            test -f build/index.html
            npm test
            '''
            }
        }
    }
}
