pipeline{
    agent any
    stages{
        stage('Git checkout SCM'){
            steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/rajatmahajan358/DSO.git']]])
                }
            }
        }
        stage('Build the project using maven'){
            steps{
                script{
                    bat 'mvnw.cmd clean package'
                }
            }
        }
        stage('Docker Image Build'){
            steps{
                script{
                    bat "docker build -t rajatmahajan/dockerregistry:\"${env.BUILD_NUMBER}\" ."
                    //dir('scripts'){
                    //    bat docker.bat ${env.BUILD_NUMBER}
                    //} 
                }
            }
        }
    }
}