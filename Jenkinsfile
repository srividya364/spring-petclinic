pipeline {
    agent {label 'spc'}
    triggers {
    pollSCM('* * * * *')
    }
    stages {
        
        stage ('git checkout') {
            steps{
                git url: 'https://github.com/spring-projects/spring-petclinic.git',
                  branch: 'main'

            }
        }
        stage ('build and scan') {
            steps {
             withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')])
                withSonarQubeEnv('SONAR') {
                sh """mvn package sonar:sonar \
                      -Dsonar.projectkey=srividya364_spring-petclinic \
                     -Dsonar.organization=srividya364 \
                     -Dsonar.host.url=https://sonarcloud.io/ \
                     -Dsonar.login=$SONAR_TOKEN"""
                 
            }
        }  
    }  
 }

}
