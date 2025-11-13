pipeline{
    agent{
        label 'Dev_Node'
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
                curl -u "$USER:$PASS" -O http://3.26.170.41:8081/repository/helloworld_release/com/rushi/hello-world/0.0.2/hello-world-0.0.2.jar
                '''
                } 
            }
        }
    }
}
