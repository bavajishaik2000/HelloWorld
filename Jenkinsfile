/*pipeline {
    agent none
    stages {
        
        stage('Deploy - Staging') {
          agent any
            steps {
                echo "Deploy code"
            }
        }

        stage('deployment approval') {
          agent none
            steps {
                script{
                        timeout(time:5,unit:'MINUTES'){
                        input (id:'Deploy', message:'Deploy to production?', submitter:'bavaji', ok:'Deploy')
                      }
                  }
            }
        }

        stage('Deploy - Production') {
          agent any
            steps {
                 echo "Deployment success"
            }
        }
    }
}*/
pipeline {
    agent none
    stages {
        stage('Build') {
            agent any
            steps {
                echo 'compiling...'
            }
        }
        stage('Test') {
            agent any
            steps {
                echo 'testing...'
            }
        }
        stage('Approval') {
            // no agent, so executors are not used up when waiting for approvals
            agent none
            steps {
                script {
                    //def deploymentDelay = input id: 'Deploy', message: 'Deploy to production?', submitter: 'bavaji', parameters: [choice(choices: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], description: 'Hours to delay deployment?', name: 'deploymentDelay')]
                    //sleep time: deploymentDelay.toInteger(), unit: 'HOURS'
                    emailext (
                                subject: "Waiting for your Approval! Job: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                                body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                                <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
                                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                                to: 'bavaji.shaik2000@gmail.com'
                            )
                }
            }
        }
        stage('Deploy') {
            agent any
            steps {
                // uses https://plugins.jenkins.io/lockable-resources
                lock(resource: 'deployApplication'){
                    echo 'Deploying...'
                }
            }
        }
    }
}

  
