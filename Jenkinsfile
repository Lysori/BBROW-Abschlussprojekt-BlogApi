


pipeline {
    agent any
    environment{
        pompath = '/var/jenkins_home/workspace/BBROW/pom.xml'
    }
    stages {
        stage('mvn compile') {
            steps {
                script {
                    
                    infincompile.compile()
                    
                }
            }
        }
        stage('mvn test') {
            steps {
                script {
                    
                    echo 'mvn test'
                    
                }
            }
        }
        stage('Package and deploy to Nexus') {
            steps {
                script {
                    
                    echo 'Package and deploy to Nexus'
                    
                }
            }
        }
        stage('mvn Install') {
            steps {
                script {
                    
                    echo 'mvn Install'
                    
                }
            }
        }
     stage('Docker Image') {
            steps {
                script {
                    
                  echo 'Docker Image'
                    
                }
            }
        }
     stage('Docker Push') {
            steps {
                script {
                    
                  echo 'Docker Push'
                    
                }
            }
        }
     stage('Deployment to Tomcat') {
            steps {
                script {
                    
                    echo 'Deployment to Tomcat'
                    
                }
            }
        }
        
    }
}
