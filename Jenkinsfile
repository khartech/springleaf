pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }
    environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    }
    stages {
        stage('Build Jar') {
            steps {
                // Run Maven on a Unix agent.
               sh 'mvn clean package'
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
        stage('Docker Build') {
            steps {
                sh "docker build khanblpr/fullstack:${TAG}"
            }
        }
       
        
        
    }
}
