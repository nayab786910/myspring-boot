pipeline{
  agent {label 'login_page'}
    stages{
        stage('CHECKOUT GIT'){
            steps{
                git branch: 'main', url: 'https://github.com/nayab786910/myspring-boot.git'
            }
        }
        stage('CODE QUALITY'){
            steps{
                script{
                    withSonarQubeEnv('sonarqube_cred'){
                        if(fileExists("sonar-project.properties")) {
                         sh "mvn sonar:sonar"
                         }
                    }
                }
            }
        }
       stage('Build Image') 
       {
          agent { label 'login_page'}
          steps{
              script {
                myImage = docker.build registry
              }
           }
        }

    }
}
