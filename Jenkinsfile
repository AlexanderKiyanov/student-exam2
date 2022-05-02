pipeline {

	agent {
		docker {
			image "hello-world"
			label 'ssh-docker-agent'
		}
	}
	
	stages {
		stage("startup") {
			echo '---------------------- startup --------------------------'
		}
	}
}
