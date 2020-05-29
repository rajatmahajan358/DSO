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
                   withDockerRegistry(credentialsId: '95689e16-1a30-4abd-a68d-66c6d6e88976', url: 'https://registry.hub.docker.com') {
                       bat "docker push rajatmahajan/smpregistry:\"${env.BUILD_NUMBER}\""
                   }                       
                }
            }
        }
    }
}