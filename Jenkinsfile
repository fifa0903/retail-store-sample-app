def branch = "main"
def remote = "origin"
def directory1 = "~/retail-store-sample-app/dist/docker-compose"
def directory2 = "~/retail-store-sample-app"
def server = "nobody1305@34.124.165.216"
def cred = "credentials"
def image1 = "nobody1305/redis:6-alpine"
def image2 = "nobody1305/mariadb:10.9"
def image3 = "nobody1305/rabbit:3-management"
def image4 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-assets:0.4.0"
def image5 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-checkout:0.4.0"
def image6 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-orders:0.4.0"
def image7 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-cart:0.4.0"
def image8 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-catalog:0.4.0"
def image9 = "nobody1305/public.ecr.aws/aws-containers/retail-store-sample-ui:0.4.0"
def image10 = "nobody1305/amazon/dynamodb-local:1.20.0"
def image11 = "redis:6-alpine"
def image12 = "mariadb:10.9"
def image13 = "rabbit:3-management"
def image14 = "public.ecr.aws/aws-containers/retail-store-sample-assets:0.4.0"
def image15 = "public.ecr.aws/aws-containers/retail-store-sample-checkout:0.4.0"
def image16 = "public.ecr.aws/aws-containers/retail-store-sample-orders:0.4.0"
def image17 = "public.ecr.aws/aws-containers/retail-store-sample-cart:0.4.0"
def image18 = "public.ecr.aws/aws-containers/retail-store-sample-catalog:0.4.0"
def image19 = "public.ecr.aws/aws-containers/retail-store-sample-ui:0.4.0"
def image20 = "amazon/dynamodb-local:1.20.0"

pipeline{
    agent any
    stages{
        stage('docker compose down'){
            steps{
                sshagent([cred]){
                    sh """ssh -tt -o StrictHostKeyChecking=no ${server} << EOF
		    cd ${directory1}
		    docker compose down 
                    exit
                    EOF"""
                    }
                }
            }
        stage('pull repository'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server}<< EOF
                    cd ${directory2}
                    git pull ${remote} ${branch}
                    exit
                    EOF"""
                    }
                }
            }

        stage('docker compose up'){
            steps{
                sshagent([cred]){
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory1}
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
                    cd ${directory1}
		    docker login
		    docker tag ${image11} ${image1}
                    docker push ${image1}
                    docker tag ${image12} ${image2}
                    docker push ${image2}
                    docker tag ${image13} ${image3}
                    docker push ${image3}
                    docker tag ${image14} ${image4}
                    docker push ${image4}
                    docker tag ${image15} ${image5}
                    docker push ${image5}
                    docker tag ${image16} ${image6}
                    docker push ${image6}
                    docker tag ${image17} ${image7}
                    docker push ${image7}
                    docker tag ${image18} ${image8}
                    docker push ${image8}
                    docker tag ${image19} ${image9}
                    docker push ${image9}
                    docker tag ${image20} ${image10}
                    docker push ${image10}

                    exit
                    EOF"""
                    }
                }
            }
        }
    }
