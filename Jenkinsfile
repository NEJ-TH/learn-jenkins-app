

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
