pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.6.1-jdk-8-slim'
            }

          }
          steps {
            sh '''echo "Building the server code..."
mvn --version
mkdir -p target
touch "target/server.war"'''
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
            sh '''echo "Buildinf the client code..."
npm install --save react
nkdir -p dist
cat > dist/index.html <<EOF
Hello!
EOF
touch "dist/client.js"'''
          }
        }
      }
    }
  }
}