pipeline {

	agent {
		label 'ssh-docker-agent'
	}
	
	stages {
		stage("build") {
			steps {
				echo '---------------------- start build and start --------------------------'			
				
				sh '''#!/bin/bash -x
							
				docker run -it -dp 8888:80 --name cont1 -w /student-exam2/ python:3.8-slim-buster
				docker cp . cont1:/student-exam2/
				
				docker exec -it cont1 pip install -e .
				docker exec -d --env FLASK_APP=js_example cont1 python3 -m flask run --host=0.0.0.0 --port=80

				curl 127.0.0.1:8888
				
				docker rm --force cont1
				
				'''
				echo '----------------------- end build and start ---------------------------'			
			}
		}
		stage("test") {
			steps {
				echo '---------------------- start testing --------------------------'			
				
				sh '''#!/bin/bash -x
				
				docker run -it -dp 8888:80 --name cont1 -w /student-exam2/ python:3.8-slim-buster
				docker cp . cont1:/student-exam2/
				
				docker exec -it cont1 pip install -e '.[test]'
				docker exec -it cont1 coverage run -m pytest
				docker exec -it cont1 coverage report

				
				'''
				echo '----------------------- end testing ---------------------------'			
			}
		}
	}
}
