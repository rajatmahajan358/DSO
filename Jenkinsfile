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
                    dir("scripts") {
                        echo "Hello"
                        bat 'build.bat'
                    }
                    mvnw.cmd clean package
                }
            }
        }
    }
}