pipeline {
  agent any
  environment {
    DEPLOY_NAMESPACE = "jx-staging"
  }
  stages {
    stage('I am here') {
      steps {
         sh 'echo I am here'
      }
    }

    stage('Stage one') {
      steps {
  			parallel {
  				stage('Execute job 1') {
  					agent {
  						label 'linux'
  					}
  					steps {
  						sh 'echo "Job 1 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				}
  				stage('Execute job 2') {
  					agent {
  						label 'linux'
  					}
  					steps {
  						sh 'echo "Job 2 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				}
  				stage('Execute job 3') {
  					agent {
  						label 'linux'
  					}
  					steps {
  						sh 'echo "Job 3 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				}
  			}
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
