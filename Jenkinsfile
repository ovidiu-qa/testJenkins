def handleCheckout = {
	sh "echo 'Checking out a merge request…'"
	checkout ([
		$class: 'GitSCM',
		branches: scm.branches,
		extensions: [
				[$class: 'PruneStaleBranch'],
				[$class: 'CleanCheckout']
		],
		userRemoteConfigs: scm.userRemoteConfigs
	])
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
