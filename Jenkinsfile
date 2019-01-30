pipeline {
  agent { node { label 'jenkins-agent' } } 
   stages {
    stage ('Run playbook') {
     steps {
        sh """
        mkdir -p roles
        ansible-galaxy install -p roles -r requirements.yml
        ansible-playbook -i inventory playbook.yml
        """
       }
      }
	   stage ('Wait for nginx restart'){
	     steps {
                     def sleep_time = 5
                     sleep sleep_time.toInteger() // seconds
		   }
	   }
	stage ('Http - request'){
	 steps{
		 script {
		    def nginx_ip = sh(script: "docker inspect --format '{{ .NetworkSettings.IPAddress }}' nginx-balancer", returnStdout: true)
                    //I want to get the same response here
                    def response = sh(script: 'curl -Is ' + nginx_ip + ' | head -1', returnStdout: true)
                    echo '=========================Response===================' + response
      }	 
     }
    }    
   }
  }
