pipeline {
    agent {
        node {
            label 'docker-agent-node'
        }
    }
    
     parameters {
        choice(name: 'ENVIRONMENT', choices: ['desarrollo', 'pruebas', 'produccion'], description: 'Selecciona el ambiente objetivo')
    }

    
    stages {
        
       stage('Solicitar Ambiente') {
            steps {
                script {
                    if (params.ENVIRONMENT) {
                        echo "Ambiente seleccionado: ${params.ENVIRONMENT}"
                    } else {
                        input message: 'Seleccione el ambiente de despliegue', parameters: [choice(name: 'ENVIRONMENT', choices: ['desarrollo', 'pruebas', 'produccion'])]
                    }
                }
            }
        }
        
       stage('Approval') {
            steps {
                // Deploy your application

                input(message:'anetas deployment approval')

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
