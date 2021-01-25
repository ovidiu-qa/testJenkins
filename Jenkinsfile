pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Pulling....'+env.BRANCH_NAME
      }
    }

    stage('Test 3: Master') {
      when {
        branch 'master'
      }
      steps {
        echo 'I only execute on the master branch.'
      }
    }

    stage('WhenTestStop') {
      when {
        branch 'testing'
      }
      steps {
        script {
          error "This pipeline stops here!"
        }

      }
    }

    stage('Testing') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing'
            script {
              if (env.BRANCH_NAME == 'master') {
                echo 'I only execute on the master branch'
              } else {
                echo 'I execute elsewhere'
              }
            }

          }
        }

        stage('Integration Testing') {
          steps {
            echo 'Integration testing'
          }
        }

        stage('Performance Testing') {
          steps {
            timeout(time: 90) {
              echo 'Performance testing complete'
            }

          }
        }

      }
    }

    stage('Merge') {
      when {
        branch 'dev'
      }
      steps {
        sh '''
          git branch -a
          git branch -r
          git branch
        '''
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying'
      }
    }

  }
  environment {
    SonarCubeScannerLocal = 'D:\\sonar-scanner-4.5.0.2216-windows\\bin'
  }
}
