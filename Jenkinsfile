pipeline {

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("build") {
      steps {
        echo 'building the app'

        cd ~/workspace/cicd-exam
        pipenv --rm
        pipenv shell

        pip install -e '.[test]'

        coverage run -m pytest
        coverage report
      }
    }

    stage("test") {
      steps {
        echo 'testing the app'
      }
    }

    stage("deploy") {
      steps {
        echo 'deploying the app'
      }
    }
  }
}
