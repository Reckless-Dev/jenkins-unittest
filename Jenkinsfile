pipeline {
	agent any
	stages {
		stage('Configure GitHub') {
      steps {
      	script {
        	// Set global Git identity using Jenkins environment variables
          bat 'git config --global user.name "${GITHUB_NAME}"'
          bat 'git config --global user.email "${GITHUB_EMAIL}"'
        }
      }
    }
 		stage('Merge to Master') {
    	steps {
        script {
          bat "git checkout master"
          bat "git merge --no-ff origin/${BRANCH_NAME}"
          bat "git push origin master"
        }
    	}
		}
  }
	post {
    success {
        echo 'Success!'
    }
    failure {
         echo 'Failed!'
    }
  }
}