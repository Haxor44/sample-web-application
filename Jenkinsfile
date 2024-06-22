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
		
            }	       	     	         
}