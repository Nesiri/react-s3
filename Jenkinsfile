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
        stage("Deploy S3"){
          agent{
                docker {
                 image 'amazon/aws-cli'
                  reuseNode true
                 args '--entrypoint=""'
                }
           }
            environment {
                AWS_DEFAULT_REGION = 'us-east-2'
            }
           steps{
                withCredentials([usernamePassword(credentialsId: 'S3-ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                        sh '''
                            echo "Testing AWS CLI"
                            aws s3 sync build/ s3://${practisebucket-s3} --delete # use this if name has - {}
                        '''
                   }
               
              
            
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