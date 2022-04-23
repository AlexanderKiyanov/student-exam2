pipeline {

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("build") {
      steps {
        echo 'building the NEW app GO!'

	sh '''#!/bin/bash -x
	mkdir -p ~/.virtualenvs
	export WORKON_HOME=~/.virtualenvs
        cd ~/workspace/cicd-exam
        pipenv --rm
        pipenv shell
	
	echo -------------------------- install test -----------------------------
	export FLASK_APP=js_example
        pip install -e '.[test]'
	
	echo ---------------------------- run test -------------------------------
        coverage run -m pytest
        coverage report
        '''
      }
    }

    stage("test") {
      steps {
        echo 'testing the NEW app'
      }
    }

    stage("deploy") {
      steps {
        echo 'deploying the NEW app'
      }
    }
  }
}
