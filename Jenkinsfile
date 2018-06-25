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
      steps {
  			parallel (
  				a: {
  					node {
  						// Run commands here -- maybe output the hostname and then run a Docker container
  						sh 'echo "Job 1 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				},
  				b: {
  					node {
  						// Run commands here -- maybe output the hostname and then run a Docker container
  						sh 'echo "Job 2 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				},
  				c: {
  					node {
  						// Run commands here -- maybe output the hostname and then run a Docker container
  						sh 'echo "Job 3 running in instance $(hostname) on node $(cat /etc/machine-id)"'
  					}
  				}
  			)
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
