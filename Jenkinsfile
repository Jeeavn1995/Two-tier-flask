pipeline {
    agent any
    stages {
        stage("clone") {
            steps {
                git url: "https://github.com/Jeeavn1995/Two-tier-flask.git", branch: "master"
            }
        }
        stage("build images") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("image push to dockerhub") {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: "dockerHubCreds",
                        passwordVariable: "dockerHubPass",
                        usernameVariable: "dockerHubUser"
                    )
                ]) {
                    sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                    sh "docker image tag two-tier-flask-app ${dockerHubUser}/two-tier-flask-app:latest"
                    sh "docker push ${dockerHubUser}/two-tier-flask-app:latest"
                }
            }
        }
        stage("run the container"){
            steps{
                sh "docker-compose up -d --build flaskapp"
            }
        }
    }
}
