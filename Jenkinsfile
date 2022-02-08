pipeline {
  agent any
  stages {
    
    stage('Promote to Dev?') {
      steps {
        milestone 10
        script {
          env.DO_RELEASE = input(
            message: 'Promote to Dev?',
            ok: 'Apply',
            parameters: [
              choice(name: 'Promote', choices: ['Yes', 'No'].join('\n'), description: 'Promote to Dev?')
            ]
          )
        }
        milestone 20
       }
    }
    
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
