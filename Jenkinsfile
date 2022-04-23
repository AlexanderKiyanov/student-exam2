pipeline {
	
    environment {
        // pipenv
        PIPENV_YES="true"
        PIPENV_NOSPIN="YES"
        PIPENV_VENV_IN_PROJECT="true"
	WORKON_HOME=~/.virtualenvs
	FLASK_APP=js_example
    }

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("build") {
      steps {
	      
        echo ---------------------- recreate virtualenv --------------------------

	sh '''#!/bin/bash -x
	mkdir -p ~/.virtualenvs
        cd ~/workspace/cicd-exam
        pipenv --rm
	pipenv install
        '''
      }
    }

    stage("test") {
      steps {
        echo -------------------------- install test -----------------------------
	
	sh '''#!/bin/bash -x
        pipenv run pip install -e '.[test]'
	
	echo ---------------------------- run test -------------------------------
        pipenv run coverage run -m pytest
        pipenv run coverage report
        '''
      }
    }

    stage("deploy") {
      steps {
        echo 'deploying the NEW app'
      }
    }
  }
}
