pipeline {
  agent {
    label "jenkins-maven"
  }
  options {
    skipDefaultCheckout true
  }

  environment {
    DEPLOY_NAMESPACE = "jx-staging"
  }
  stages {
  	stage('I am here') {
  		steps {
  		 sh 'echo I am here'
  		}
  	}
    stage('Copy The Website') {
  		steps {
  		 sh 'gsutil rsync -R . gs://hackday.rak01.com'
  		}
  	}
  }
}
