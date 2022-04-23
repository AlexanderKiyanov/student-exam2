pipeline {

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("install test") {
      steps {
	      
        echo '---------------------- recreate virtualenv --------------------------'

	sh '''#!/bin/bash -x
	mkdir -p ~/.virtualenvs
        cd ~/workspace/cicd-exam
	export WORKON_HOME=~/.virtualenvs
	export FLASK_APP=js_example
        pipenv --rm
	pipenv install
        '''
      }
    }

    stage("run test") {
      steps {
        echo '-------------------------- install test -----------------------------'
	
	      
	sh '''#!/bin/bash -x
	
	export WORKON_HOME=~/.virtualenvs
	export FLASK_APP=js_example
	
        pipenv run pip install -e '.[test]'
	
	echo '---------------------------- run test -------------------------------'
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
