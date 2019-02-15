pipeline {
  agent { node { label 'jenkins-agent' } } 
   stages {
    stage ('Run playbook') {
     steps {
        sh """
        mkdir -p roles
        ansible-galaxy install -p roles -r requirements.yml
	ansible-vault decrypt ssh/ansible --vault-password-file=/home/jenkins/pass
	ansible-vault decrypt ssh/ansible.pub --vault-password-file=/home/jenkins/pass
	ansible-vault decrypt ssh/known_hosts --vault-password-file=/home/jenkins/pass
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
