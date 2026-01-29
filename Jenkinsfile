pipeline{
  agent { 
        label 'dev' 
    }
  environment{
    SCANNER_HOME = tool "sonar"
  }
  stages{

    stage("Clean Workspace"){
      steps{
        cleanWs()
      }
    }
    
    stage("code"){
      steps{
        git url :"https://github.com/Ajinkya-Giri27/Expenses-Tracker-WebApp.git/" , branch : "main"
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

stage('Dependency Check') {
    steps {
        dependencyCheck additionalArguments: '''
            --scan .
            --format HTML
            --out dependency-check-report
            --disableAssembly
        ''',
        odcInstallation: 'dc'

        dependencyCheckPublisher pattern: 'dependency-check-report/dependency-check-report.html'
    }
}


    stage('Trivy Filesystem Scan') {
    steps {
        sh '''
          trivy fs \
            --format template \
            --template "@html.tpl" \
            --output trivy-fs-report.html \
            .
        '''
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
