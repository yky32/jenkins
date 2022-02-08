pipeline {
  agent any
  stages {
    
    stage('Start Test?') {
      steps {
        echo 'Start build'
      }
    }
    
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            input(message: 'Start?', ok: 'Yes')
            echo 'Start Test'
          }
        }

        stage('Test 2') {
          steps {
            echo 'Test 2'
          }
        }

        stage('Test 3') {
          steps {
            echo 'Test 3'
          }
        }

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
