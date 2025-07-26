pipeline{
    agent any;
    stages{
        stage("clone git"){
            steps{
                git url: "https://github.com/Jeeavn1995/Two-tier-flask.git", branch: "master"
            }
        }
        stage("build"){
            steps{
                sh "docker compose up -d"
            }
        }
        
    }    
}
