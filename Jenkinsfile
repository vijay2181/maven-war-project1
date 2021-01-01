pipeline {
  agent {label 'label11'}
stages {

  stage('git-checkout') {    //this is a sample commit
  steps {
git 'https://github.com/vijay2181/maven-war-project1.git'
           }
}
  
  stage('environment-setting') {
             steps {
                  script {
                       env.BUILD = "yes" // Setting env variable for Build 
                             }
                       }
                 }


   stage('Build')  {

   when {environment name: 'BUILD', value: 'yes'}
   steps { 
               echo "Building artifacts ..."
               sh "mvn clean package "
               }

             }
  
  
  
}
}
