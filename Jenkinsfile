pipeline{
 agent any 
stages {
   stage('Checkout Code'){
     steps{
           echo "Cloning repository from Github"
           git branch:'master', url:'https://github.com/Curiousgoal202/New-Jenkins-file1.git'
         }
       }
    stage('Build workspace'){
      steps {
          echo "Preparing workspace"
          sh ''' 
          rm -rf "$WORKSPACE/devops-web-project"
          mkdir -p  "$WORKSPACE/devops-web-project/"
          cp index.html about.html contact.html README.md "$WORKSPACE/devops-web-project/"
         cp -r assets "$WORKSPACE/devops-web-project/"
          '''
         }
       }
    stage('Run Web Server'){
        steps {
            echo "Starting the web server on port 8085"
           sh '''
           fuser -k 8085/tcp || true 
           nohup python3 -m http.server 8085 --directory $WORKSPACE/devops-web-project > /dev/null 2>&1 &
           disown
            '''
            }
         }
  }
    post {
        success {
              echo "website deployed successfully at http://54.183.178.164:8085"
                 }
       failure {
             echo "Deployment failed, Check logs" 
              }
        }
}
  



