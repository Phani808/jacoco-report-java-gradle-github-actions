pipeline {
   agent any
    options {
    skipDefaultCheckout()
  }

   stages {
    stage("Checkout") {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: "main"]],
          userRemoteConfigs: [[url: "$https://github.com/Phani808/jacoco-report-java-gradle-github-actions.git"]]
        ])
      }
    }
   }
}    