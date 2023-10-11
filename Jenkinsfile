pipeline{
  agent any 
  tools {
    maven 'maven'
  }
  stages {
    stage ("Clean up"){
      steps {
        deleteDir()
      }
    }
    stage ("Clone repo"){
      steps {
        sh "git clone https://github.com/chernihou/devopsangular.git"
      }
    }
    stage ("Generate backend image"){
      steps{
        dir("devopsangular/springboot"){
          sh "mvn clean install"
          sh "docker build -t devopsangular ."
        }
      }
    }
    stage ("Build Angular"){
  steps {
    dir("devopsangular/angular-app"){ 
      sh "npm install"  
      sh "ng build --prod"  
    }
  }
}
    stage ("Run docker compose"){
      steps { 
        dir("devopsangular"){
        sh "docker compose up -d"
      }}}}}
