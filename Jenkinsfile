pipeline {
    agent any
    
    stages {
        stage('Maven install') {
            steps {
                bat 'mvn clean install -DskipTests'
            }
        }
        stage('Deploy Docker Tomcat container') {
            steps {
                bat """docker kill Deploy2
                        docker build . -t test2
                        docker run --rm -d -p 90:8080 --name Deploy2 test2"""
            }
        }
	stage ('[TEST]Deployment') {
	
    	def var1 = bat(script: '@curl --write-out %%{http_code} --silent --location --output nul http://localhost:90/spring-mvc-example', returnStdout: true)
    	if(var1 =='200') 
        {echo 'Test Passed!\n Access the App from http://localhost:90/spring-mvc-example/'}
	    else {
	        echo '[ERROR] Application deployment was unsuccesful'
	     
	    
	}	
        }
        
    }   
}
