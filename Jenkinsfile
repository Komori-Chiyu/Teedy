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
        }
      }
    }
        stage('Generate PMD') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          sh 'mvn pmd:pmd'
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
    archiveArtifacts artifacts: '**/target/surefire-reports/**/', fingerprint: true
    archiveArtifacts artifacts: '**/target/pmd.html/', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
    archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
  }
}
}
