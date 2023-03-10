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
     stage("Run Test Coverage") {
      steps {
        sh "./gradlew jacocoTestReport"
      }
    }
     stage("Generate JaCoCo Badge") {
      steps {
        script {
          def jacocoBadgeGenerator = docker.image("cicirello/jacoco-badge-generator:v2")
          jacocoBadgeGenerator.run([
            "--generate-branches-badge", "true",
            "--jacoco-csv-file", "build/reports/jacoco/test/jacocoTestReport.csv"
          ])
        }
      }
    }
   }
}    