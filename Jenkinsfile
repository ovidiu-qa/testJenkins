pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Pulling...' + env.BRANCH_NAME
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing'
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
        }
        steps {
            withSonarQubeEnv('LocalSonarQubeServer') {
                sh '''
                ${scannerHome}/bin/sonar-scanner.bat \
                -Dsonar.host.url=http://127.0.0.1:9000 \
                -Dsonar.projectKey=local.testJenkins \
                -Dsonar.projectName=TestJenkinsMe  \
                -Dsonar.sources=D:/Jenkins/workspace/testJenkins_'+${env.BRANCH_NAME}+'
                '''
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
