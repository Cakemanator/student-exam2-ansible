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
	stage ('Http - request'){
	 steps{
		 script {
                    //I want to get the same response here
                    def response = sh(script: 'curl -Is 172.17.0.8 | head -1', returnStdout: true)
                    echo '=========================Response===================' + response
      }	 
     }
    }    
   }
  }
