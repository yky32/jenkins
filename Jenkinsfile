pipeline {
  agent any
  stages {
    stage('Testing branch name?') {
      steps {
        milestone 10
        script {
          if (env.CHANGE_BRANCH) {
            if (env.CHANGE_BRANCH.startsWith("hotfix/")) {
              env.DO_RELEASE='Yes'
              echo 'its hotfix/ ' + env.CHANGE_BRANCH + env.DO_RELEASE
            } else {
              env.DO_RELEASE='No'
              echo 'its hotfix/ ' + env.CHANGE_BRANCH + env.DO_RELEASE
            }
          }
        }
        milestone 20
      }
    }
   
    stage("Env Variables") {
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
          environment name: 'DO_RELEASE', value: 'No' 
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
