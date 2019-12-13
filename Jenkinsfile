pipeline {
  agent {
    docker {
      image 'maven:3.3.9_jdk_8'
    }

  }
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.5-jdk-8-slim'
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

  }
}