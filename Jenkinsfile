def branch = "main"
def remote = "origin"
def directory = "~/retail-store-sample-app"
def server = "nobody1305@34.124.165.216"
def cred = "heehe"

pipeline{
    agent any
    stages{
        stage('repo pull'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
		    docker compose down
                    cd ${directory}
                    git pull ${remote} ${branch}
                    exit
                    EOF"""
                    }
                }
            }

	 stage('docker build'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker build -t faizal-frontend .
                    exit
                    EOF"""
                    }
                }
            }

        stage('docker compose'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker compose up -d
                    exit
                    EOF"""
                    }
                }
            }
	
	 stage('docker push'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
		    docker tag faizal-frontend:latest ${image}
                    docker push ${image}
                    exit
                    EOF"""
                    }
                }
            }
        }
    }
