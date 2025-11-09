pipeline{
    agent{
        label 'dev_node'
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
            }
        }
    }
}
