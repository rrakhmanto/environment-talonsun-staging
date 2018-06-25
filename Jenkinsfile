pipeline {
  agent {
    label "google-sdk"
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
  		 sh 'curl https://sdk.cloud.google.com | bash && gsutil rsync -R . gs://hackday.rak01.com && gsutil acl ch -u AllUsers:R gs://hackday.rak01.com/index.html'
  		}
  	}
  }
}
