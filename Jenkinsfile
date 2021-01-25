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
          git commit --author="QA test <ovidiu.fulea@quantum-alchemy.com>"
          git merge origin/branch-2
        '''
        
      }
    }
  }
}
