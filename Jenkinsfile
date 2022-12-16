pipeline{
  agent {label 'login_page'}
    tools {maven "MAVEN"}
    stages{
        stage('code checkout from GitHub'){
            steps{
                git branch: 'master', url: ''
            }
        }
        stage('Code Quality Check via SonarQube'){
            steps{
                script{
                    def scannerHome = tool 'sonarqube-scanner';
                    withSonarQubeEnv(credentialsId: 'sonarqube_access_token'){
                        if(fileExists("sonar-project.properties")) {
                         sh "${tool("sonarqube-scanner")}/bin/sonar-scanner"
                         }
                    }
                }
            }
        }
    }
}
