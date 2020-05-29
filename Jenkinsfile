pipeline{
    agent any

    environment{
        registry = "rajatmahajan/smpregistry"
        registryCredential = 'Dockerhub'
    }

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
                    bat "docker build -t rajatmahajan/smpregistry:\"${env.BUILD_NUMBER}\" ."
                    //dir('scripts'){
                    //    bat docker.bat ${env.BUILD_NUMBER}
                    //} 
                }
            }
        }
        stage('Image push to hub'){
            steps{
                script{
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"  
                    docker.withRegistry( 'https://registry.hub.docker.com/v1/', registryCredential ) {
                        dockerImage.push()
                    } 
                }
            }
        }
    }
}