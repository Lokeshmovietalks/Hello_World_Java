pipeline{
    agent{
        docker{
            image 'maven'
            args '-u 0 -v $HOME/.m2:/root/.m2'
        }
    }
    stages{
        stage('github checkout'){
            steps{
                git url: 'https://github.com/Lokeshmovietalks/Hello_World_Java.git', branch: 'master'
            }
        }
        stage('maven build'){
            steps{
                sh 'mvn clean compile jib:build -Dimage=paps0903/helloworld:oct27'
            }
        }
    }
}
