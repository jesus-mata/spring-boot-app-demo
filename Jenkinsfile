pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "M3"
   }
   
   stages {
      stage('checkout') {
         steps {
         	checkout scm
      
         	echo 'branch name ' + env.BRANCH_NAME

                echo sh(script: 'env|sort', returnStdout: true)
         }
      }
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            //git 'https://github.com/ChuyAMS/spring-boot-app-demo.git'

            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean package"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
   }
}
