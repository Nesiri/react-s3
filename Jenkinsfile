pipeline{
    agent any
    environment{
        NODE_ENV = 'production'
        NETLIFY_PROJECT_ID ="a93937ad-d751-494d-ac5a-541f0095e053"
        NETLIFY_AUTH_TOKEN = credentials('EC2_Token')
    }
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
            stage("Deploy"){
                agent{
                    docker{
                        image 'node:20-alpine'
                        reuseNode true
                    
                    }
            }
                steps{
                    sh '''
                        npm install netlify-cli -g
                        netlify deploy --prod --dir=dist --site=$NETLIFY_PROJECT_ID --auth=$NETLIFY_AUTH_TOKEN
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