pipeline {
  agent any
  stages {
    
    stage("list all when PR-merged in") {
      steps {
         sh "printenv" 
      }
    }
    
    
    stage('Testing branch name?') {
      steps {
        milestone 1
        script {
          if (env.CHANGE_BRANCH.contains("hotfix/")) {
            env.DO_RELEASE='Yes'
            echo 'its hotfix/ ' + env.CHANGE_BRANCH + env.DO_RELEASE
          } else {
            env.DO_RELEASE='No'
            echo 'its hotfix/ ' + env.CHANGE_BRANCH + env.DO_RELEASE
          }
        }
        milestone 9
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
