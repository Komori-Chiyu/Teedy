pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'mvn -B -DskipTests clean package'
        }
      }
    }
    stage('Test') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'mvn test'
          sh 'mvn site'
        }
      }
    }
    stage('Generate Javadoc') {
      steps {
        sh 'mvn javadoc:jar'
      }
    }
  }

  post {
  always {
    archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
  }
}
}
