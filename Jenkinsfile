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
        '''
      }
    }
  }
}
