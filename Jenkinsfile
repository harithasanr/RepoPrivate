pipeline {
    agent any
    
    tools {
          maven "MAVEN_HOME"
            jdk "JAVA_HOME"
    }
stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                         bat 'xcopy target\\*.war "C:\\Program Files\\Apache Software Foundation\\Tomcat 10.1\\webapps" /Y'
                       // deploy adapters: [tomcat9(credentialsId: 'tomcat', path: 'C:/Program Files/Apache Software Foundation/Tomcat 10.1/webapps', url: 'http://localhost:8080/')], contextPath: null, war: '**/*.war'
                        //sh "scp -v -o StrictHostKeyChecking=no **/*.war root@${params.staging_server}:/opt/tomcat/webapps/"
                    }
                }
            }
        }
    }
}
