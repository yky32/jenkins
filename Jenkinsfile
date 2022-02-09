pipeline {
  agent any
  stages {
    stage('Is Hotfix?') {
      steps {
        milestone 10
        script {
          env.DO_RELEASE = input(
            message: 'Is Hotfix?',
            ok: 'Apply',
            parameters: [
              choice(name: 'Promote', choices: ['Yes', 'No'].join('\n'), description: 'Promote to Dev?')
            ]
          )
        }
        milestone 20
      }
    }
    
    stage("Env Variables of J") {
      when { 
        beforeAgent true; 
        anyOf { 
          branch 'main'; 
        } 
      }
      steps {
         sh "printenv" 
      }
    }

    stage('Test') {
      when { 
        beforeAgent true; 
        allOf { 
          environment name: 'DO_RELEASE', value: 'NO' 
        } 
      }
      parallel {
        stage('Test') {
          steps {
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
      when { 
        beforeAgent true; 
        allOf { 
          branch 'PR-*'
          environment name: 'DO_RELEASE', value: 'Yes' 
        } 
      }
      steps {
        echo 'Start build ' + env.GITHUB_PR_SOURCE_BRANCH
      }
    }

    stage('Notify') {
      steps {
        echo 'Finished'
      }
    }

  }
}
