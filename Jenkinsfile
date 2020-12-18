pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Pulling....' + env.BRANCH_NAME
      }
    }
    stage ('Test 3: Master') {
        when { branch 'master' }
        steps { 
            echo 'I only execute on the master branch.' 
        }
    }
    stage('WhenTestStop') {
       when { branch 'testing' }
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
    stage('SonarQube') {
        environment {
            scannerHome = tool 'SonarCubeScannerLocal'
            somethingElse = 'TEST';
        }
        steps {
            withSonarQubeEnv('LocalSonarQubeServer') {
                sh """
                ${scannerHome}/bin/sonar-scanner.bat \
                -Dsonar.host.url=http://127.0.0.1:9000 \
                -Dsonar.projectKey=local.testJenkins.${env.BRANCH_NAME} \
                -Dsonar.projectName=TestJenkinsMe[${env.BRANCH_NAME}] \
                -Dsonar.sources=D:/Jenkins/workspace/testJenkins_${env.BRANCH_NAME}
                """
            },
            def qq = waitForQualityGate()
            if(qq.status != 'OK') {
              error "Pipeline aborted due to quality gate failure: ${qq.status}"
            }
        }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying'
      }
    }

  }
}
