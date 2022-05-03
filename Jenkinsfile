pipeline {

	agent {
		label 'ssh-docker-agent'
	}
	
	environment {
		DOCKERHUB_PASS=credentials('dockerhub-pass')
	}
	
	stages {
		stage("startup") {
			steps {
				echo '---------------------- start startup --------------------------'			
				
				sh '''#!/bin/bash -x
							
				docker run -it -dp 8888:80 --name cont1 -w /student-exam2/ python:3.8-slim-buster
				docker cp . cont1:/student-exam2/
				
				docker exec -it cont1 pip install -e .
				docker exec -d --env FLASK_APP=js_example cont1 python3 -m flask run --host=0.0.0.0 --port=80
				
				docker rm --force cont1
				
				'''
				echo '----------------------- end startup ---------------------------'			
			}
		}
		
		stage("test") {
			steps {
				echo '---------------------- start testing --------------------------'			
				
				sh '''#!/bin/bash -x
				
				docker run -it -dp 8888:80 --name cont1 -w /student-exam2/ python:3.8-slim-buster
				docker cp . cont1:/student-exam2/
				
				docker exec cont1 pip install -e '.[test]'
				docker exec cont1 coverage run -m pytest
				docker exec cont1 coverage report

				docker rm --force cont1
				
				'''
				echo '----------------------- end testing ---------------------------'			
			}
		}
		
		stage("build image") {
			steps {
				echo '---------------------- start build image --------------------------'			
				
				sh '''#!/bin/bash -x
				
				cat > Dockerfile <<- EOF
				FROM python:3.8-slim-buster
				COPY . /student-exam2/
				WORKDIR /student-exam2
				RUN pip install -e .
				ENV FLASK_APP=js_example
				CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=80"]
				EXPOSE 80/tcp
				EOF

				docker build -t alexanderkiyanov/appimg:latest .
				
				docker run -it -dp 8888:80 --name cont1 alexanderkiyanov/appimg:latest
				
				'''
				echo '----------------------- end build image ---------------------------'			
			}
		}
		
		stage("docker hub") {
			steps {
				echo '---------------------- start push to docker hub --------------------------'			
				
				sh '''#!/bin/bash -x
				
				docker images
				echo $DOCKERHUB_PASS | docker login -u alexanderkiyanov --password-stdin
				docker push alexanderkiyanov/appimg:latest
				
				docker rm --force alexanderkiyanov/appimg:latest
				
				'''
				echo '----------------------- end push to docker hub ---------------------------'			
			}
		}
	}
}
