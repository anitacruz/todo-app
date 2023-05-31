pipeline {
    agent {
        node {
            label 'docker-agent-node'
        }
    }

    triggers {
        githubPush() // Trigger the pipeline on GitHub push events
    }
    
    stages {
        stage('Fetch') {
            steps{ 
                echo "Fetching 💡"
                sh'''
                    git clone https://github.com/szavalia/todo-app
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