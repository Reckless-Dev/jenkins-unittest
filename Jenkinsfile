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
		
 		stage("composer_install") {
			steps {
				echo 'composer install...'
 				bat 'composer install'
			}
		}

		stage("phpunit") {
			steps {
				echo 'running the phpunit test...'
				bat './vendor/bin/phpunit tests/Unit'
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