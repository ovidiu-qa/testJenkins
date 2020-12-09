pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'echo \'Bulding here two\''
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
                sh '''${scannerHome}/bin/sonar-scanner.bat \
                -Dsonar.host.url=http://127.0.0.1:9000 \
                -Dsonar.projectKey=local.testJenkins \
                -Dsonar.projectName=TestJenkinsMe  \
                -Dsonar.sources=http://127.0.0.1:8080/job/testJenkins/job/master/ '''
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
