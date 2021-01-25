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
            commit: '--author="QA test"'
        sh '''          
          git merge origin/branch-1
        '''
        
      }
    }
  }
}
