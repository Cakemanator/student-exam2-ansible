pipeline {
  agent { node { label 'jenkins-agent' } } 
   stages {
    stage ('Run playbook') {
     steps {
        sh """
        mkdir roles
        ansible-galaxy install -p roles -r requirements.yml
        ansible-playbook -i inventory playbook.yml
        """
       }
      }
    }
  }
  
