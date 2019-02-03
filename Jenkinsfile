pipeline {
  agent { node { label 'jenkins-agent' } } 
   stages {
    stage ('Run playbook') {
     steps {
        sh """
        mkdir -p roles
        ansible-galaxy install -p roles -r requirements.yml
	ansible-vault decrypt ssh/ansible --vault-password-file=/home/jenkins/pass
        ansible-playbook -i inventory playbook.yml
        """
       }
      }
	   stage ('Wait for nginx restart'){
		   steps {
                     sleep 5 // seconds
	    }
	   }
	stage ('Http - requests'){
	 steps{
		 script {
		    def nginx_ip = sh(script: "docker inspect --format '{{ .NetworkSettings.IPAddress }}' nginx-balancer", returnStdout: true)
                    //I want to get the same response here
                    def response = sh(script: 'curl -s ' + nginx_ip + ' | grep hostname' , returnStdout: true)
                    echo response
		    def response = sh(script: 'curl -s ' + nginx_ip + ' | grep hostname' , returnStdout: true)
                    echo response
		    def response = sh(script: 'curl -s ' + nginx_ip + ' | grep hostname' , returnStdout: true)
                    echo response
      }	 
     }
    }    
   }
  }
