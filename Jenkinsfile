pipeline {
  agent any
  stages {
    stage('Merge') {
      when {
        branch 'dev'
      }
      steps {
        sh '''
          git branch -a
          git branch: 'unit-testing-ovidiu', 
                credentialsId: 'QA_GitHub_FO',  
                url: 'https://github.com/ovidiu-qa/testJenkins'
                git branch -a
        '''
        
      }
    }
  }
}
