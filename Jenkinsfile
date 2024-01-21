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
       
        stage("zabbix-postgres") {
            steps {
                sh '''
                docker build -t zabbix-postgres -f Dockerfile.postgres .
                '''
            } 
        }
        stage("zabbix-server") {
            steps {
                sh '''
                docker build -t zabbix-server -f Dockerfile.server .
                '''
            } 
        }
        stage("zabbix-web") {
            steps {
                sh '''
                docker build -t zabbix-web -f Dockerfile.web .
                '''
            } 
        }


    
                
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'yurashupikjenkins', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
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