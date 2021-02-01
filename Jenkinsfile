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
          sh('git remote -v')
          sh('git push https://ovidiu-qa:Quantum33$$@master')
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