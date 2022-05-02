pipeline {

	agent {
		label 'ssh-docker-agent'
	}
	
	stages {
		stage("startup") {
			steps {
				echo '---------------------- startup --------------------------'			
				
				sh '''#!/bin/bash
				docker ps
				docker run hello-world
				echo $PATH
				'''
			}
			
		}
	}
}
