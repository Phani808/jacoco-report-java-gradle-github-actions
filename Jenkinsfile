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
  stages {
        stage('Generate JaCoCo Badge') {
            steps {
                // Use the cicirello/jacoco-badge-generator plugin to generate the badge.
                // You can adjust the plugin version to suit your needs.
                // Note that this plugin requires that you have JaCoCo set up in your project.
                // Refer to the plugin documentation for more information.
                steps {
                    script {
                        def jacocoCsvFile = "build/reports/jacoco/test/jacocoTestReport.csv"
                        def generateBranchesBadge = true

                        sh "docker run --rm -v $(pwd):/app cicirello/jacoco-badge-generator:v2 --input $jacocoCsvFile --branches $generateBranchesBadge"

                    }
                }
            }
        }
       } 
           }           |   