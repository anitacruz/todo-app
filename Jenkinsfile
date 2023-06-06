pipeline {
    agent {
        node {
            label 'docker-agent-node'
        }
    }
    
    stages {
        
       stage('Select environment') {
            steps {
                script {
                    env.AMBIENTE = input message: 'Select deployment environment', parameters: [choice(name: 'ENVIRONMENT', choices: ['dev', 'stg', 'prod'])]
                    echo "selected environment : ${ambiente}"
                }
            }
        }
        
       stage('Approval') {
            steps {
                // Deploy your application

                input(message:'Do you approve the following deploy?')

                // Only continue if approved by specific users
//                 script {
//                     input('deployment-approval', submitter='acruz')
//                     if (!approvers == 'admin'  && !approvers=='acruz') {
//                         error("Deployment not approved by authorized users")
//                     }
//                 }
            }
        }
       
        stage ('Deploy'){
            steps{
                script {
                    if(env.AMBIENTE == 'dev'){
                        echo "Deploy to dev"
                    }
                    else if (env.AMBIENTE == 'stg'){
                        echo "Deploy to dev"
                        echo "Deploy to stg"
                    }
                    else if (env.AMBIENTE == 'prod'){
                        echo "Deploy to dev"
                        echo "Deploy to stg"
                        echo "Deploy to prod"
                    }
                    else{
                        echo "abort"
                    }
                }
            }      
        }
        
         stage('Fetch') {
            steps{ 
                echo "Fetching 💡"
                sh'''
                    git clone https://github.com/anitacruz/todo-app
                '''
            } 
        }
        stage('Test') {
            steps { 
                echo "Testing ️🥊"
                sh '''
                cd todo-app
                yarn
                yarn test
                '''
            }
        }
        stage('Build') {
            steps {
                // You can add your build steps here
                echo "Building 🛠️"
                sh '''
                cd todo-app
                yarn build
                '''
            }
        }
    }
}
