pipeline {
   agent any
   options {
         buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3')
         }

   stages {
            stage('Checkout SCM') {
                steps {
                git branch: 'main', url: 'https://github.com/Phani808/jacoco-report-java-gradle-github-actions.git'
        }       
      }
       stage("Grant execute permission for gradlew") {
      steps {
        sh "chmod +x gradlew"
      }
    }
     stage("Run Tests") {
      steps {
        sh "./gradlew test"
      }
    }
     stage('Test') {
      steps {
        sh './gradlew clean test jacocoTestReport'
      }
    }
  }
  post {
    always {
      jacoco(execPattern: '**/build/jacoco/*.exec')
      archiveArtifacts(artifacts: '**/build/jacoco/*.xml')
      junit '**/build/test-results/test/*.xml'
    }
  }
} 