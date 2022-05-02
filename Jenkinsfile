pipeline {

	agent {
		label 'ssh-docker-agent'
	}
	
	stages {
		stage("startup") {
			steps {
				echo '---------------------- startup --------------------------'			
				docker ps
				docker run hello-world
			}
			
		}
	}
}
