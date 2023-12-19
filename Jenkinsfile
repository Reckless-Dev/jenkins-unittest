pipeline {
	agent any
	stages {
		stage('Deployment') {
			steps {
				// Create an Approval Button with a timeout of 15minutes.
	    	// timeout(time: 15, unit: "MINUTES") {
	    		input message: 'Do you want to approve the deployment?', ok: 'Yes'
	    	// }

				echo "Initiating deployment"
	  	}
		}

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
					withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
            bat 'git clean -fdx'
            bat "git checkout master"
          	bat "git pull https://${GITHUB_TOKEN}@github.com/Reckless-Dev/jenkins-unittest.git master" // Pull changes from the remote master
          	bat "git merge --no-ff origin/${BRANCH_NAME}"
          	bat "git push https://${GITHUB_TOKEN}@github.com/Reckless-Dev/jenkins-unittest.git master"
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