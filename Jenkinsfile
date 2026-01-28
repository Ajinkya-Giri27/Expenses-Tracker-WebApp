pipeline{
  agent { 
        label 'dev' 
    }
  environment{
    SCANNER_HOME = tool "sonar"
  }
  stages{

    
    stage("code"){
      steps{
        git url :"https://github.com/Ajinkya-Giri27/Expenses-Tracker-WebApp.git/" , branch : "main"
      }
    }

    
stage('Clean Package') {
    steps {
        sh '''
        chmod +x mvnw
        ./mvnw clean package -DskipTests
        '''
    }
}
    
    stage("SonarQube Analysis"){
      steps{
        
        withSonarQubeEnv("sonar")
        {
          sh " rm -rf .scannerwork || true "
          sh "chmod +x mvnw"
          sh "./mvnw clean package -DskipTests"
          sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Expenses-tracker -Dsonar.projectKey=Expensese-tracker "
        }
      }
    }

  
    

    stage("Build"){
      steps{
        sh "docker build -t expenses-tracker ."
      }
    }
    
    stage("Push to Docker Hub"){
      steps{
       withCredentials([usernamePassword(
         credentialsId : "dockerHubCreds" ,
         passwordVariable : "dockerHubPass" ,
         usernameVariable : "dockerHubUser"
         )]){

         sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
         sh "docker image tag expenses-tracker ${env.dockerHubUser}/expenses-tracker"
         sh "docker push ${env.dockerHubUser}/expenses-tracker:latest"
       }
      }
    }

   stage("Deploy"){
      steps{
        sh "docker compose up -d"
      }
    }


    
  }
}
