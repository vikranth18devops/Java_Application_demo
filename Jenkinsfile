pipeline{
    agent any 
    
    stages{
        stage("sonar quality check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'Sonar1') {
                            sh 'chmod +x gradlew'
                            sh './gradlew sonarqube'
                    }

                  timeout(time: 1, unit: 'HOURS') 

                }  
            }
        }
        
        
        
        
        
        
    }

    
}
