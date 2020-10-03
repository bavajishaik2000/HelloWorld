pipeline{
agents none
stages{
stage("Build"){
agents any
steps{
  step{
  echo "Build successful"
  }
  }
  }
stage("test"){
steps{
agents any
  step{
  echo "test successful"
  }
  }
  }
  stage("approval"){
  agents none
steps{
script{
timeout(time:5,unit:'MINUTES'){
input (id:'Deploy', message:'Deploy to production?', submitter:'bavaji', ok:'Deploy')
}
   }
  }
  }
  stage("production"){
steps{
agents any
  step{
  echo "production successful"
  }
  }
  }
  }
  }
