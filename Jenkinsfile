pipeline {
    agent any
    tools {
        maven 'localMaven'
    }

    parameters {
         string(name: 'tomcat_stag', defaultValue: '10.0.0.116', description: 'Tomcat Staging Server')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Deployments') {
            steps {
                script {
                    sh "scp **/*.war jenkins@${params.tomcat_stag}:/usr/share/tomcat/webapps"
                }
            }
        }
    }
}

