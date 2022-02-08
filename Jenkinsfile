pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        echo 'Start Test'
        input 'Skip?'
      }
    }

    stage('Building') {
      steps {
        echo 'Start build'
      }
    }

    stage('Notify') {
      steps {
        echo 'Finished'
      }
    }

  }
}