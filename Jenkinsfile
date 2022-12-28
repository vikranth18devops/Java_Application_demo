pipeline{
    agent any 
    environment{
        VERSION = "${env.BUILD_ID}"
    }
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

                   

                }  
            }
        }
        stage("docker build & docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                             sh '''
                                docker build -t 20.12.200.148:8083/aarvik:${VERSION} .
                                docker login -u admin --password-stdin $docker_password 20.12.200.148:8083 
                                docker push  20.12.200.148:8083/aarvik:${VERSION}
                                docker rmi 20.12.200.148:8083/aarvik:${VERSION}
                            '''
                    }
                }
            }
        }
        
        
       
    }

   
}

