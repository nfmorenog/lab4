pipeline {
  agent none
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          steps {
            sh '''echo "Building the server"
'''
          }
        }

        stage('Client') {
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
          steps {
            sh 'echo \'gradle test -Dbrowser=chrome\''
          }
        }

        stage('firefox') {
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