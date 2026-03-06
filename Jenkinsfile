pipeline {
    agent {label 'spc'}
    parameters {
        choice(name:'goals',choices:['package','clean install','verify'],description:'pick something')
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
             withCredentials([string(credentialsId: 'SONAR', variable: 'SONAR_TOKEN')])
                withSonarQubeEnv('SONAR') {
                sh """mvn ${ params.goals} sonar:sonar \
                      -Dsonar.projectkey=srividya364_spring-petclinic \
                     -Dsonar.organization=srividya364 \
                     -Dsonar.host.url=https://sonarcloud.io/ \
                     -Dsonar.login=$SONAR_TOKEN"""
                 
            }
        }  
    }  
 }

}
