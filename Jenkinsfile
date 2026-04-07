pipeline{
    agent any
    stages{
        stage("Build"){
            agent{
                docker{
                    image 'node:20-alpine'
                    reuseNode true
                
                }
           }
            steps{
                sh '''
                    npm install
                    npm run build
                    ls -la
                '''
            }
           
        }

        stage("Test"){
            agent{
                docker{
                    image 'node:20-alpine'
                    reuseNode true
                
                }
           }
            steps{
                sh '''
                    npm install
                    npm test
                '''
            }
           
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}