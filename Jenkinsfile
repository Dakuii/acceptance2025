pipeline {
    agent any
    stages {
        stage("Package") {
            steps {
                sh "./gradlew build"
            }
        }
        
        stage("Docker build") {
            steps {
                sh "docker build -t localhost:5000/calculatrice ."
            }
        }
        
        stage("Docker push") {
            steps {
                sh 'docker push localhost:5000/calculatrice'
            }
        }
        
        stage("Deploy to staging ou Déployer en préproduction") {
            steps {
                // Cleanup previous container if it exists
                sh "docker rm -f calculatrice || true"

                // Check if port 8888 is already in use
                script {
                    def portOccupied = sh(script: "lsof -i :8888", returnStatus: true) == 0
                    if (portOccupied) {
                        echo "Port 8888 is already in use. Changing to a different port."
                        // If port 8888 is occupied, try using port 9999 or another available one
                        sh "docker run -d --rm -p 9999:8081 calculatrice localhost:5000/calculatrice"
                    } else {
                        // If port is not occupied, use port 8888
                        sh "docker run -d --rm -p 8888:8081 calculatrice localhost:5000/calculatrice"
                    }
                }
            }
        }
        
        stage("Acceptance test") {
            steps {
                sleep 60
                sh "chmod +x acceptance_test.sh && ./acceptance_test.sh"
            }
        }
    }
}

