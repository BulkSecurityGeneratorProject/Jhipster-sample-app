pipeline {
  agent any
  stages {
    stage('Initilize') {
      steps {
        sh '''
      echo "PATH = ${PATH}"
      echo "MAVEN_HOME = ${MAVEN_HOME}"
      '''
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        stash(name: 'war', includes: 'target/**')
      }
    }
    stage('Backend') {
        steps {
          parallel(
          'Unit' : {
            unstash 'war'
            sh mvn -B -DtestFailureIgnore test || exit 0'
            junit '**/surefire-reports/**/*.xml'
          },
          'performance' : {
           unstash 'war'
          sh '# ./mvn -B gatling:execute'
          })
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
  tools {
    maven 'maven-3.9'
  }
}