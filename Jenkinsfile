pipeline {

  agent {
    label 'ssh-docker-agent'
  }

  stages {
    stage("build") {
      steps {
        echo 'building the app1'
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
