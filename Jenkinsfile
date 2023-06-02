pipeline {
    agent {
        node {
            label 'docker-agent-node'
        }
    }

    
    stages {
        
       
        
       stage('Approval') {
            steps {
                // Deploy your application

                input('anetas deployment approval', submitter:'acruz')

                // Only continue if approved by specific users
//                 script {
//                     input('deployment-approval', submitter='acruz')
//                     if (!approvers == 'admin'  && !approvers=='acruz') {
//                         error("Deployment not approved by authorized users")
//                     }
//                 }
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
