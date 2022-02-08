pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        input(message: 'Start?', ok: 'Yes')
        echo 'Start Test'
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