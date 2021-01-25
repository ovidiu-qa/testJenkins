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
          git merge origin/master
          git check origin/master
          git push
        '''

      }
    }
  }
}