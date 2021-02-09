#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc)

pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    stages {
        // implicit checkout stage

        stage('Build') {
            steps {
                sh './mvnw -Dhttp.proxyHost=http.proxy.fmr.com -Dhttp.proxyPort=8000 -Dhttps.proxyHost=http.proxy.fmr.com -Dhttps.proxyPort=8000 package'
            }
        }
    }
    // post after stages, for entire pipeline, is also an implicit step albeit with explicit config here, unlike implicit checkout stage
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
    }
}
