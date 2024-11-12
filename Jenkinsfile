pipeline {
    agent any
    stages {
    
    stage("Package"){
    	steps{
    	sh "./gradlew build"
    	}
    }
    
    stage("Docker build"){
    	steps{
    	sh "docker build -t localhost:5000/calculatrice ."
    	}
    }
    
    stage("Docker push"){
    	steps{
	sh 'docker push localhost:5000/calculatrice'
    	}
    }
    
    stage("Deploy to staging ou Déployer en préproduction"){
    	steps{
	sh "docker run -d --rm -p 8888:8081 calculatrice localhost:5000/calculatrice"
    	}
    }
       
     
     
     
}
}

