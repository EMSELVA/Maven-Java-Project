def ansible = [:]
         ansible.name = 'ansible'
         ansible.host = '172.31.19.55'
         ansible.user = 'centos'
         ansible.password = 'Rnstech@123'
         ansible.allowAnyHosts = true
def kops = [:]
         kops.name = 'kop'
         kops.host = '172.31.23.238'
         kops.user = 'centos'
         kops.password = 'Rnstech@123'
         kops.allowAnyHosts = true
pipeline {
    agent { label 'buildserver'}

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3"
    }

    stages {
        stage('Prepare-Workspace') 
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'build', url: 'https://github.com/EMSELVA/Maven-Java-Project.git'   
		stash 'Source'
            }
            
        }
        stage('Tools-Setup') {
            steps {
		   echo "Tools Setup"
                sshCommand remote: ansible, command: 'cd Maven-Java-Project; git pull'
                //sshCommand remote: ansible, command: 'cd Maven-Java-Project; ansible-playbook -i hosts tools/sonarqube/sonar-install.yaml'
                sshCommand remote: ansible, command: 'cd Maven-Java-Project; ansible-playbook -i hosts tools/docker/docker-install.yml'   
        
                 }            
        }
	  
    }
}
