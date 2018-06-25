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

    stage('Stage one') {
		parallel {
			stage('Execute job 1') {
				agent {
					label 'jenkins-maven'
				}
				steps {
					sh 'echo "Job 1 running in instance $(hostname) on node $(cat /etc/machine-id)"'
				}
			}
			stage('Execute job 2') {
				agent {
					label 'jenkins-nodejs'
				}
				steps {
					sh 'echo "Job 2 running in instance $(hostname) on node $(cat /etc/machine-id)"'
				}
			}
			stage('Execute job 3') {
				agent {
					label 'jenkins-python'
				}
				steps {
					sh 'echo "Job 3 running in instance $(hostname) on node $(cat /etc/machine-id)"'
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
