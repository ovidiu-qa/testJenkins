pipeline {
  agent any
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
          git branch -a
          git merge remotes/origin/dev
<<<<<<< HEAD
          git push
=======
          git push --set-upstream origin master
>>>>>>> master
        '''

      }
    }
  }
}