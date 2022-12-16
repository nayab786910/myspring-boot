pipeline{
  agent {label 'login_page'}
      environment {
        registry = "519852036875.dkr.ecr.us-east-1.amazonaws.com/my-first-ecr"
    }
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
        stage('BUILDING ARTIFACT'){
          agent { label 'login_page_1'}
     			 steps{
        			  echo 'build '
                sh "mvn clean package"
     			  }
        }
        stage('DOCKER IMAGE') 
       {
          agent { label 'login_page_1'}
          steps{
              script {
                myImage = docker.build registry
              }
           }
        }

    }
}
