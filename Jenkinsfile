pipeline{

      agent any
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('sonarserver') { 
					withMaven(
						maven: 'maven-3'
					){
						sh "mvn sonar:sonar"
					}
					
			      
                       	     	}
							withMaven(
						maven: 'maven-3'
					){
						sh "mvn clean install"
					}
		    	    
		  
                 	}
               	 }  
              }

			  stage('Docker build'){
				steps{
					script{
						def dockerHome = tool 'docker'
        				env.PATH = "${dockerHome}/bin:${env.PATH}"
						sh 'docker build . -t haxor44/java-web:latest'
						withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
							
							sh 'docker login -u evolmalek04@gmail.com -p $docker_password'
							sh 'docker push haxor44/java-web:latest'
						}
					}
				}
			  }	
		
            }	       	     	         
}