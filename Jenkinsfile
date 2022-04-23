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
    
    node {
      sh 'ls -l'
      dir ('foo') {
        writeFile file:'dummy', text:''
      }
      sh 'ls -l'
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
