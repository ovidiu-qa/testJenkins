pipeline {
  agent any
  parameters {
      string(name: 'GITPAS', defaultValue: 'Quantum33$$', description: 'Git Pas')
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
          sh('git checkout dev https://github.com/ovidiu-qa/testJenkins')
          sh('git merge https://github.com/ovidiu-qa/testJenkins@master')
          sh('git add . && git commit - m "update" https://github.com/ovidiu-qa/testJenkins@dev')
          sh('git push https://github.com/ovidiu-qa/testJenkins@dev')
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