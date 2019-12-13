pipeline {
  agent none
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'gradle:6.0.1-jdk-8'
            }

          }
          steps {
            sh '''echo "Building the server"
'''
            stash(name: 'server', includes: '**/*.war')
          }
        }

        stage('Client') {
          agent {
            docker {
              image 'node:6'
              args '-u 0:0'
            }

          }
          steps {
            sh '''echo "Building the client"
'''
          }
        }

      }
    }

    stage('Test') {
      parallel {
        stage('chrome') {
          agent {
            docker {
              image 'selenium/standalone-chrome'
            }

          }
          steps {
            sh 'echo \'gradle test -Dbrowser=chrome\''
          }
        }

        stage('firefox') {
          agent {
            docker {
              image 'selenium/standalone-firefox'
            }

          }
          steps {
            sh 'echo \'gradle test -Dbrowser=firefox\''
          }
        }

        stage('iOS') {
          steps {
            sh 'echo "test en iOS"'
          }
        }

      }
    }

    stage('Develop') {
      steps {
        sh 'echo "En desarrollo"'
      }
    }

    stage('Deploy') {
      steps {
        sh 'echo "en produccion" '
      }
    }

  }
}