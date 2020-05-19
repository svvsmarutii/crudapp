node('slave'){
    stage('codeFetch') {
        container('jenkins-slave'){
            jobname = sh(returnStdout: true,script:"echo \${JOB_URL} |  rev | cut -d'/' -f 4 | rev").toString().trim()
            git branch: env.BRANCH_NAME, credentialsId: 'githubcredmaru', url: 'https://github.com/svvsmarutii/crudapp.git'
            container('maven') {
                stage('Build') {
                    configFileProvider([configFile(fileId: 'e15dea1f-e7d5-453e-aacf-ed6e5ac6c2ed', variable: 'MySettings')]) {
                        sh 'mvn -s ${MySettings} clean install'
                        sh 'find /root/.m2 -maxdepth 3 -type d'
                    }    
                }
            }
        }
    }
}
