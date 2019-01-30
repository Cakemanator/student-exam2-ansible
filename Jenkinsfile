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
		 sh "echo ${curl -Is localhost:5001 | head -1}"
	 }
    }    
   }
  }
