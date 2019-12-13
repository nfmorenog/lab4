pipeline {
  agent {
    docker {
      image 'maven:3.3.9-jdk-8'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.5.2-jdk-8'
            }

          }
          steps {
            sh '''echo "Building the server"
mvn -version
mkdir -p tarjet
touch "tarjet/server.war"'''
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
npm install --save react
mkdir -p dist
cat > dist/index.html <<EOF
Hello!
EOF
tocuh "dist/client.js"'''
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
            sh 'echo \'mvn test -Dbrowser=chrome\''
          }
        }

        stage('firefox') {
          agent {
            docker {
              image 'selenium/standalone-firefox'
            }

          }
          steps {
            sh 'echo \'mvn test -Dbrowser=firefox\''
          }
        }

      }
    }

  }
}