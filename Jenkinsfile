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
                script {
                    if (isUserAdmin()) {
                        input(message: 'Proceed with the deployment?', submitter: 'admin')
                    } else {
                        error('You are not authorized to approve the pipeline.')
                    }
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

def isUserAdmin() {
    def userId = Jenkins.instance.getAuthentication().getName()
    return userId == 'admin' || userId == 'acruz'
}
