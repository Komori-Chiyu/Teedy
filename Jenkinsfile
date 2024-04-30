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
        sh 'mvn site' // 生成项目报告，包括pom报告和javadoc
      }
    }
    stage('Generate Javadoc') {
      steps {
        sh 'mvn javadoc:jar'
      }
    }
  }
}
