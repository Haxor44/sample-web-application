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
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
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