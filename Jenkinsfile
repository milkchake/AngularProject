pipeline{
    
    agent any
    
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }
    
      environment { 
       DOCKERHUB_CREDENTIALS = credentials('docker-hub')
    }
    
 stages{
    
    stage('Git') {
        
        steps('Cloning'){
            
        git branch : 'main',
                // Get some code from a GitHub repository
                url: 'https://github.com/milkchake/AngularProject.git'

                // Get System Current Date
                script{
                    Date date = new Date()
                    String dateString = date.format("dd-MM-yyyy")
                    println "Date : " + dateString
                }
        }
    }
        
   
   stage('Building Docker image') { 
            steps { 
               sh 'docker build -t milqshake/angular .'
}
            } 
        
           stage('login to dockerhub') {
            steps{
               
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR -p ****'
            }
           }
           
        stage('Push Docker image') { 
            steps { 
                sh 'docker push milqshake/angular:latest'
}

            
        } 
    
   

    /* stage('Cleaning up') { 
        steps { 
            sh "docker rmi $registry:$BUILD_NUMBER" 
        }
    }*/


}

}



