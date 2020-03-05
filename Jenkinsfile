pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "Mymaven"
   }

   stages {
        stage('Build') {
           steps {
            // Get some code from a GitHub repository
            git branch: 'develop', credentialsId: 'BitbucketCredentials_Maruthi', url: 'http://172.30.102.152:7990/scm/crud/crudapp.git'

            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean package"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
           }
        }
}
