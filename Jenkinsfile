pipeline {
  agent any
  stages {
<<<<<<< HEAD
    stage('Merge') {
      when {
        branch 'dev'
      }
=======
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

            // mail(subject: 'Testing', body: 'Hello Blue Ocea', from: 'bluea-ocean@quantum-alchemy.com', replyTo: 'bluea-ocean@quantum-alchemy.com', to: 'ovidiu.fulea@quantum-alchemy.com')
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
      steps {
        sh (script: "git branch -a")
      }
    }
    stage('Deploy') {
>>>>>>> branch-1
      steps {
        git branch: 'dev', 
            credentialsId: 'QA_GitHub_FO',  
            url: 'https://github.com/ovidiu-qa/testJenkins'            
        sh '''
          git merge origin/master
        '''
        
      }
    }
  }
}