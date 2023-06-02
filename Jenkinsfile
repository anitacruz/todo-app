pipeline {
    agent {
        node {
            label 'docker-agent-node'
        }
    }

    
    stages {
        
        stage('Fetch') {
            steps{ 
                echo "Fetching 💡"
                sh'''
                    git clone https://github.com/anitacruz/todo-app
                '''
            } 
        }
        
       stage('Approval') {
            steps {
                // Deploy your application

                // Prompt for approval
                input(id: 'deployment-approval', message: 'Approve deployment?', parameters: [
                [$class: 'ChoiceParameterDefinition', choices: 'user1,user2,user3', name: 'Approver']
                ])

                // Only continue if approved by specific users
                script {
                    def approvers = input('deployment-approval')
                    if (!approvers.contains('user1') && !approvers.contains('user2') && !approvers.contains('user3')) {
                    error("Deployment not approved by authorized users")
                }
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
