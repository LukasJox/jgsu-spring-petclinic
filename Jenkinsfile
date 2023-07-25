#!groovy

pipeline {
    agent any
    triggers {
        pollSCM('H/15 * * * *')
    }
    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/LukasJox/jgsu-spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                bat './mvnw package'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
