pipeline{
    agent any
    environment{
        NODE_ENV = 'production'
        NETLIFY_PROJECT_ID ="a93937ad-d751-494d-ac5a-541f0095e053"
        NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
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
                         npm install netlify-cli
                            ls -la build
                        netlify deploy
                         --prod \
                          --dir=build \ 
                          --site=$NETLIFY_PROJECT_ID \
                          --auth=$NETLIFY_AUTH_TOKEN\
                           --no-build \
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