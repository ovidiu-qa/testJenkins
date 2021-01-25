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
          git pull
          git checkout origin/master
          git merge origin/dev
          git push
          git checkout origin/dev
        '''

      }
    }
  }
}