pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        stash name: 'war', includes: 'target/**'
      }
    }
    stage('Unit') {
      parallel {
        stage('Backend') {
          steps {
            sh 'echo Test'
          }
        }
        stage('Perfromance Test') {
          steps {
            sh 'echo perfomance test'
          }
        }
      }
    }
    stage('Frontend') {
      steps {
        sh 'echo Frontend'
      }
    }
    stage('Static Analysis') {
      steps {
        sh 'echo Static Analysis'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploy'
      }
    }
  }
}