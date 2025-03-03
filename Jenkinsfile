pipeline{
    
    agent { label "dev"};
    
    stages{
        stage("Code Clone"){
            steps{
                echo "hello dosto"
                git url: "https://github.com/AbhishekChauhan1101/two-tier-flask-app.git", branch: "master"
               
            }
        }
        stage("Build"){
            steps{
                sh "whoami"
                sh "docker build -t two-tier-flask-app ."
            }
            
        }
        stage("Test"){
            steps{
                echo "Developer / Tester tests likh ke dega..."
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword
                (credentialsId:"dockerHubCreds", 
                usernameVariable: "DOCKER_USERNAME",
                passwordVariable: "DOCKER_PASSWORD"
                )]){
                    sh "docker login -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}"
                    sh "docker image tag two-tier-flask-app ${env.DOCKER_USERNAME}/two-tier-flask-app"
                    sh "docker push  ${env.DOCKER_USERNAME}/two-tier-flask-app:latest"
                
                }  
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}


