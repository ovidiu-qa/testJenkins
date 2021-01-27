pipeline {
  agent any
  parameters {
      gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
  }
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
        '''

      }
    }
    stage("list all branches")
        {
            steps
            {
                git branch: "${params.BRANCH}", credentialsId: "QA_GitHub_FO", url: "https://github.com/ovidiu-qa/testJenkins"
                git branch -a
            }
        }
  }
}