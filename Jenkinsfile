pipeline {
  agent any
   stages {
  // Mark the code checkout 'stage'....
  stage ('Stage SCM'){
    steps {
  // Checkout code from repository and update any submodules
  git 'https://github.com/badredaha/pivaa.git'  
}

  }
  
  stage('Running Tests') {
      steps {
        parallel (
          "Unit Tests": {
            sh 'fastlane test'
          }
        )
      }
    }

stage('Running Build') {
      steps {
        parallel (
          "Build Project": {
            sh 'fastlane build'
          }
        )
      }
    }
    
     stage('Running Metrics') {
       steps {
        parallel (
          "Check Dependency": {
            sh 'fastlane checkdependency'
          },"Sonar Metrics": {
            sh 'fastlane metrics'
          }
        )
      }  
  
    }

    stage('Documentation') {
      steps {
      sh 'fastlane documentation'
      }
    }
  

  stage ('Security'){

  steps {
    sh 'bash script_sec.sh'
  }
  }

   stage ('Prepro'){
   
 steps {
      sh 'fastlane beta'
      }
   }

   stage ('Prod'){
    
    steps {
      sh 'fastlane prod'
      }
   }
}
}
