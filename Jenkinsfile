node('slave'){
    stage('codeFetch') {
        container('jenkins-slave'){
            git branch: env.BRANCH_NAME, credentialsId: 'githubcredmaru', url: 'https://github.com/svvsmarutii/crudapp.git'
            container('maven') {
                stage('Build') {
                    //jobname = sh(returnStdout: true,script:"echo \${JOB_URL} |  rev | cut -d'/' -f 4 | rev").toString().trim()
                    echo jobname
                    configFileProvider([configFile(fileId: 'e15dea1f-e7d5-453e-aacf-ed6e5ac6c2ed', variable: 'MySettings')]) {
                        jobname = "crudapp"
                        sh 'mvn -s ${MySettings} clean install'
                        sh 'find /root/.m2 -maxdepth 3 -type d'
                    }    
                }
            }
        }
    }
}
