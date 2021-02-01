pipeline {
  agent any
  parameters {
      QA_GitHub_FO = "Quantum33$$"
  }
  stages {
    stage('Merge') {
      when {
        branch 'master'
      }
      steps {
        git branch: 'master',
            credentialsId: 'QA_GitHub_FO',
            url: 'https://github.com/ovidiu-qa/testJenkins'
        sh '''
          git branch -v -a
        '''
      }
    }
    stage('Merge 1') {
      when {
        branch 'master'
      }
      steps {
        withCredentials([usernamePassword(credentialsId: 'QA_GitHub_FO', passwordVariable: 'key', usernameVariable: 'gitUser')]) {
          sh("git branch -v -a https://ovidiu-qa:${QA_GitHub_FO}@github.com/ovidiu-qa/testJenkins")
        }
      }
    }
  }
   post() {
      always {
        withCredentials([usernamePassword(credentialsId: 'QA_GitHub_FO', passwordVariable: 'key', usernameVariable: 'gitUser')]) {
        sh '''
          git branch -v -a
        '''
        }
      }
    }
}