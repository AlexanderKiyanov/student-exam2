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
	export WORKON_HOME=/var/.virtualenvs
        cd ~/workspace/cicd-exam
        pipenv --rm
        pipenv shell
        pip install -e '.[test]'
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
