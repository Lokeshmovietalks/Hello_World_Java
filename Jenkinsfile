pipeline{
    agent{
        label 'Node_1'
        }
    stages{
        stage('github-checkout'){
            steps{
                git url: 'https://github.com/Lokeshmovietalks/Hello_World_Java.git', branch: 'master'
            }
        }
        stage('maven build'){
            steps{
                sh 'mvn -v'
                sh 'mvn clean package'
            }
        }
        stage('Nexus Deploy'){
            steps{
                sh 'mvn deploy'
            }
        }
        stage('Nexus Download'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'nexus-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]){
                    sh '''
                echo "Downloading jar form nexus"
                curl -u "$USER:$PASS" -O http://13.211.254.233:8081/repository/helloworld_release/com/rushi/hello-world/0.0.3/hello-world-0.0.3.jar
                '''
                } 
            }
        }
        /*stage('Docker Build'){
            steps{
                sh '''
                echo "Building Docker image"
                docker build -t $DOCKUSER/helloworld:nov15v3 .
			#	docker run -d -p 8080:8080 helloworld:nov13v3
                '''
            }
        }*/
		stage("Docker Push"){
			steps{
				withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'DOCKUSER', passwordVariable: 'DOCKPASS')]){
					sh '''
					echo "$DOCKPASS" | docker login -u "$DOCKUSER" --password-stdin
					docker build -t $DOCKUSER/helloworld:nov19v3 .
					docker push $DOCKUSER/helloworld:nov19v3
					'''
				}
			}
		}
    }
}
