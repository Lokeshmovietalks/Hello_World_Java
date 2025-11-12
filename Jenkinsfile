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
    }
}
