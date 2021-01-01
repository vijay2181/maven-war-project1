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
  
  stage('Code Coverage') {

   when {environment name: 'BUILD', value: 'yes'}
  steps {
     echo "Running Code Coverage ..." 
	   sh "mvn  org.jacoco:jacoco-maven-plugin:0.5.5.201112152213:prepare-agent"
	 }
                  }
 
  stage('SonarQube Analysis')                     
  {
    when {environment name: 'BUILD', value: 'yes'}
    steps{
     withSonarQubeEnv('demosonarqube') {                                     //demosonarqube is name of sonarqube dashboard given in sonarqube servers
	  
         sh 'mvn sonar:sonar'                                                   //it will call static code analysis and capture the details
	  }
    }
  }
  
  
}
 
}
