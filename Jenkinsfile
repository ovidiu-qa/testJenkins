pipeline {
  agent any
  stages {
    stage('Merge') {
      when {
        branch 'dev'
      }
      steps {
        git branch: 'dev',
            credentialsId: 'QA_GitHub_FO',
            url: 'https://github.com/ovidiu-qa/testJenkins'
        sh '''
          git branch -a
          git checkout remotes/origin/master
          git branch -a
        '''

      }
    }
  }
}