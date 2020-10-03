pipeline {
    agent none
    stages {
        /* "Build" and "Test" stages omitted */

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
}


  
