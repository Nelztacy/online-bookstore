pipeline {
    agent any
    tools {
        maven 'localMaven'
    }

    parameters {
         string(name: 'tomcat_stag', defaultValue: '10.0.0.113', description: 'Tomcat Staging Server')
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

        stage('Deployment to Tomcat') {
            steps {
                script {
                    sh "scp **/*.war technel@${params.tomcat_stag}:/usr/share/tomcat9/webapps"
                }
            }
        }
    }
}

