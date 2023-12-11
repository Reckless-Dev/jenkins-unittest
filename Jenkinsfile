pipeline {
	agent any
	stages {
 		stage("composer_install") {
			steps {
				echo 'composer install...'
 				sh 'composer install'
			}
		}

		stage("phpunit") {
			steps {
				echo 'running the phpunit test...'
				sh './vendor/bin/phpunit tests/Unit'
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