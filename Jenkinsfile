pipeline {

	agent {
		label 'ssh-docker-agent'
	}
	
	stages {
		stage("build") {
			steps {
				echo '---------------------- start build --------------------------'			
				
				sh '''#!/bin/bash -x
							
				cat > Dockerfile <<EOF
				FROM python:3.8-slim-buster
				COPY . /student-exam2/
				WORKDIR /student-exam2
				RUN pip install -e .
				ENV FLASK_APP=js_example
				CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=80"]
				EXPOSE 80/tcp
				EOF

				docker build -t appimg:latest .
				docker run -dp 8888:80 --name appcont appimg:1.0
				curl 127.0.0.1:8888

				
				'''
				echo '---------------------- end build --------------------------'			
			}
			
		}
	}
}
