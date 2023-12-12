pipeline {
	agent any
	stages {
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