pipeline {
  agent any
  parameters {
      gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
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
        sh '''
          git branch -v -a
          git checkout dev HEAD:https://github.com/ovidiu-qa/testJenkins#dev
        '''
        }
      }
    }
  }
   post() {
      always {
        withCredentials([usernamePassword(credentialsId: 'QA_GitHub_FO', passwordVariable: 'key', usernameVariable: 'gitUser')]) {
        sh '''
          git branch -v -a
          git checkout dev HEAD:https://github.com/ovidiu-qa/testJenkins#dev
        '''
        }
      }
    }
}