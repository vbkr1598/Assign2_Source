pipeline
{
    agent any
    environment
	{
		response_code='0'
	}
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
		    sleep time: 2000, unit: 'MILLISECONDS'
            }
        }
	 stage ('[TEST]Deployment') {
		 steps{
			 echo 'Testing for HTTP response'
		 script{
    	response_code = bat(script: '@curl --write-out %%{http_code} --silent --location --output nul http://localhost:90/spring-mvc-example', returnStdout: true)
			 
			 
    	if(response_code =='200') 
        {echo 'Test Passed!\n Access the App from http://localhost:90/spring-mvc-example/'}
	    else {
	        echo '[ERROR] Application deployment was unsuccesful'}	
        }
	}
	}
	}
	post {
        always {
		echo 'This will always run RESPONSE: '+ response_code
        }
        success {
            echo 'This will run only if successful RESPONSE: '+ response_code
        }
        failure {
            echo 'This will run only if failed RESPONSE: '+ response_code
        }
        unstable {
            echo 'This will run only if the run was marked as unstable RESPONSE: '+ response_code
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed RESPONSE: '+ response_code
            echo 'For example, if the Pipeline was previously failing but is now successful RESPONSE: '+ response_code
        }
    }
}
