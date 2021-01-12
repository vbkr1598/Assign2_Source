pipeline
{
    agent any
    environment
	{
		response_code='0'
	}
    stages 
	{
        stage('Maven install')
	    {
            	steps
		    {
                	bat 'mvn clean install -DskipTests'
            	    }
	    }
        stage('Deploy Docker Tomcat container')
	    {
            steps
		{
                bat """docker kill Deploy2
                        docker build . -t test2
                        docker run --rm -d -p 90:8080 --name Deploy2 test2"""
		sleep time: 2000, unit: 'MILLISECONDS'
            	}	
	    }
	 stage ('[TEST]Deployment')
	    {
		 steps
		    {
			 echo 'Testing for HTTP response'
		 	script
			    {
    				response_code = bat(script: '@curl --write-out %%{http_code} --silent --location --output nul http://localhost:90/spring-mvc-example/pages/version.html', returnStdout: true)
			 	if(response_code =='200') echo '[SUCCESS] Test Passed!'
	    			else echo '[ERROR] Application deployment was unsuccesful!'
				 Debug()
        		    }
		    }
	     }
	}
	post 
	{
        	always
		{
			echo '[PIPELINE] This will always run once steps are completed.'
			Debug()
       		 }
       		success
		{
            		echo '[PIPELINE] This will run only if successful\n Access the App from http://localhost:90/spring-mvc-example/'
        	}
        	failure
		{
			echo '[PIPELINE] This will run only if there is failure HTTP_RESPONSE: '+ response_code
        	}
        	unstable 
		{
            		echo '[PIPELINE] This will run only if the run was marked as unstable HTTP_RESPONSE: '+ response_code
        	}
        	changed 
		{
           		echo '[PIPELINE] This will run only if the state of the Pipeline has changed HTTP_RESPONSE: '+ response_code
            		echo 'For example, if the Pipeline was previously failing but is now successful'
        	}
    	}
	def Debug()
	{
		echo 'DEBUG'
	}
}
