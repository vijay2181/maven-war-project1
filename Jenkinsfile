pipeline {
  agent {label 'label11'}  //this is a sample comment
stages {

  stage('git-checkout') {
  steps {
git 'https://github.com/vijay2181/maven-war-project1.git'
           }
}
  
  stage('environment-setting') {
             steps {
                  script {
                       env.BUILD = "yes" // Set env variable for further Build Stages
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
