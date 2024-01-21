#!groovy
//  groovy Jenkinsfile
properties([disableConcurrentBuilds()])\

pipeline  {
        agent { 
           label ''
        }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
       
        stage("zabbix") {
            steps {
                sh '''
                docker build -t zabbix-postgres -f /var/lib/jenkins/workspace/EXAM---JENKINS/Dockerfile.postgres /var/lib/jenkins/workspace/EXAM---JENKINS/
                docker build -t zabbix-server -f /var/lib/jenkins/workspace/EXAM---JENKINS/Dockerfile.server /var/lib/jenkins/workspace/EXAM---JENKINS/
                docker build -t zabbix-web -f /var/lib/jenkins/workspace/EXAM---JENKINS/Dockerfile.web /var/lib/jenkins/workspace/EXAM---JENKINS/

                '''
            } 
        }



    
                
        tage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: '2eba81a8-f30c-478f-9670-75760b456ef2', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        def loginResult = sh(script: "docker login -u $USERNAME -p $PASSWORD", returnStatus: true)
                        if (loginResult != 0) {
                            error "Failed to log in to Docker Hub. Exit code: ${loginResult}"
                        }
                    }
                }
                echo " ============== docker login completed =================="
            }
        }

        stage("docker push") {
            steps {
                echo " ============== pushing image =================="
                sh '''
                
                '''
            }
        }
    }
}