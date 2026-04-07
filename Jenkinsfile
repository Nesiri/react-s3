pipeline{
    agent any
    environment{
        NODE_ENV = 'production'
        NETLIFY_PROJECT_ID ="4d8e5b2b-4507-47ee-9127-be4377ef40a3"
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
                        npx netlify deploy --prod --dir=build --site=$NETLIFY_PROJECT_ID --auth=$NETLIFY_AUTH_TOKEN --no-build
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