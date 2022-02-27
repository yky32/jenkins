pipeline {
  agent any
  stages {
    stage('Testing branch name?') {
      steps {
        milestone 10
        script {
          if (env.CHANGE_BRANCH.contains("hotfix/")) {
            echo 'its hotfix/ ' + env.CHANGE_BRANCH
          } else {
            echo 'its not hotfix!! ' + env.CHANGE_BRANCH
          }
        }
        milestone 20
      }
    }
    
    stage('Is Hotfix? v2') {
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
    
    stage("Env Variables of Je") {
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
        echo 'Start build ' + env.CHANGE_BRANCH
      }
    }

    stage('Notify') {
      steps {
        echo 'Finished'
      }
    }

  }
}
