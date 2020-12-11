pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Pulling.....' + env.BRANCH_NAME
      }
    }

    stage('Testing') {
      parallel {
        stage('Test') {
          steps {
            echo 'Testing'
            error "This pipeline stops here!"
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
