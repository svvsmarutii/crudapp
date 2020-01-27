pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "Maruthi_Maven"
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
        stage('CopyToDestination') {
           steps {
		   sh label: '', script: '''#!/bin/bash 
              /usr/bin/expect <<EOD
              spawn scp ${WORKSPACE}/target/crudApp.war root@172.30.102.151:/opt/maruthi/tomcat/dev/webapps
              expect "password:"
              send "root1234\\r"
              expect {
                "ETA" {exp_continue}
                "100%" {}
            }'''
		   }
	    }
	}
}