pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
        sh 'mvn site'
      }
    }
  }
  post {
    always {
      stage('Generate Javadoc') {
        steps {
          sh 'mvn javadoc:jar'
        }
      }
    }
  }
}
