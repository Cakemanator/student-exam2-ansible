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
                     sleep 30 // seconds
	    }
	   }
	stage ('Http - requests'){
	 steps{
		 script {
		    def nginx_ip = sh(script: "docker inspect --format '{{ .NetworkSettings.IPAddress }}' nginx-balancer", returnStdout: true)
                    
                    def response = sh(script: 'curl -sI ' + nginx_ip, returnStdout: true)
                    echo response
      }	 
     }
    }    
   }
  }
