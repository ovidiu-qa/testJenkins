def handleCheckout = {
	sh "echo 'Checking out a merge request…'"
}

apipeline {
  agent any
  stages {
    stage('Merge') {
      when {
        branch 'dev'
      }
      steps {
        handleCheckout()
        sh '''
          git branch -a
        '''
      }
    }
  }
}
