pipeline {

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("build") {
      steps {
        echo 'building the NEW app'

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
