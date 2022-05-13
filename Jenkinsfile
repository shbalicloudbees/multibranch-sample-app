pipeline {
 agent {label 'ubuntuos'}
 options {
   buildDiscarder(logRotator(numToKeepStr: '5'))
 }
 stages {
   stage('Build') {
     steps {
       sh './gradlew clean check --no-daemon'
     }
   }

  stage('cat README') {
    when {
      branch "fix-*"
    }
     steps {
       sh '''
        cat README.md
       '''
     }
   }

 }
 post {
   always {
       junit(
         allowEmptyResults: true,
         testResults: '**/build/test-results/test/*.xml'
       )
   }
 }
}

