pipeline {
  agent {label 'label11'}
stages {

  stage('git-checkout') {
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
	   
	 }
                  }
	
	stage('SonarQube Analysis')                     
  {
    when {environment name: 'BUILD', value: 'yes'}
    steps{
     
         echo 'code analysis'                                                  //it will call static code analysis and capture the details
	  }
    }
	
  
stage("Quality Gate"){ 
    when {environment name: 'BUILD', value: 'yes'}
    steps{
	    echo 'quality gates'}
}
	
	
	stage('Stage Artifacts') 
  {          
  
   when {environment name: 'BUILDME', value: 'yes'}
   steps {          
    script { 
	    /* Define the Artifactory Server details */
        def server = Artifactory.server 'jfrog'                       //Artifactory.server is a fuction got by installing artifactory plugin
        def uploadSpec = """{
            "files": [{
                "pattern": "samplewar/target/samplewar.war",                                  
                "target": "demoCICD"                                                        
            }]
        }"""                                                                                                //demoCICD is the repository name in jfrog
        
        /* Upload the war to  Artifactory repo */
        server.upload(uploadSpec)
    }
   }
  }
	
}
}
