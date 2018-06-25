pipeline {
  agent {
    label "jenkins-maven"
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

    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
