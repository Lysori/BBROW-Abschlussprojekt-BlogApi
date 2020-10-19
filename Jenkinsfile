pipeline {
    agent any
    environment {
       BUILDYML = 'buildImage.yml'
       PUSHYML = 'loginPush.yml'
       PULLDEPLOYYML = 'pulldeployImage.yml'
    }
    stages {
        stage('mvn compile') {
            steps {
                script {
                    
                    mvn.compile() 
                    
                }
            }
        }
        stage('mvn test') {
            steps {
                script {
                    
                    mvn.test()
                    
                }
            }
        }

        stage('mvn verify/sonar') {
            steps {
                script {
                    
                    mvn.verify()
                    
                }
            }
        }

        stage('Package and deploy to Nexus') {
            steps{
                configFileProvider([configFile(fileId: 'default', variable: 'MAVEN_GLOBAL_SETTINGS')]){ 
                    script {

                        mvn.deploy()
                        
                    } 
                }
            }
        }

     stage('Pull and Build Image') {
            steps {
                script {
                    
                  ansibleplay.imagepull(BUILDYML)
                    
                }
            }
        }
    
     stage('Push Image') {
            steps {
              withCredentials([usernamePassword(credentialsId: 'AZURECR', usernameVariable: 'AZURECR_USER', passwordVariable: 'AZURECR_PASSWORD')]) {
                
                script {
                    
                  ansibleplay.imagepush(PUSHYML)
                    
                }
              }
            }
            
        }
        stage('mvn deploy on Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASSWORD')]) {
                   
                    sh 'docker build -t bbrowneutest .'
                    sh 'ansible-playbook pulldeployImage.yml -e TOMCAT_USER=$TOMCAT_USER -e TOMCAT_PASSWORD=$TOMCAT_PASSWORD'
               
                }
            }
        }
        
    }
}
