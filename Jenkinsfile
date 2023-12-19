pipeline {
	agent any

  environment {
    SSH_KEY = credentials('ec35cc0b-e77f-4603-b7fe-7aafe4002087')
  }

	stages {
		stage('Configure GitHub') {
      steps {
      	script {
        	// Set global Git identity using Jenkins environment variables
          bat 'git config --global user.name "${GIT_COMMITTER_NAME}"'
          bat 'git config --global user.email "${GIT_COMMITTER_EMAIL}"'
          
          // Configure Git to use credential helper
          bat 'git config --global credential.helper store'
        }
      }
    }
 		stage('Merge to Master') {
    	steps {
        script {
					// Auto-merge with credentials
					withCredentials([sshUserPrivateKey(credentialsId: 'ec35cc0b-e77f-4603-b7fe-7aafe4002087', keyFileVariable: 'SSH_KEY')]) {
            try {
              bat "git checkout master"
          	  bat "git pull origin master"  
          	  bat "git merge --no-ff origin/${BRANCH_NAME}"
          	  bat "git push origin master"  
            } catch (Exception e) {
              echo "Error during Git operations : ${e.message}"
              currentBuild.result = 'FAILURE'
            }
        	}
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