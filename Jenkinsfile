pipeline{
    agent any
    
    tools {
        maven 'Maven_Home'  // pass same name which is define in jenkins global configuration
    }

    stages{
        stage("Test"){
            steps{
                //mvn test
                //sh "mvn --version"
                sh "mvn test"
            }
           
        }

        stage("Build"){
            steps{
                //mvn install or package
                sh "mvn package"
            }
           
        }
        stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatServerDetails1', path: '', url: 'http://34.226.150.65:8081/')], contextPath: '/app', war: '**/*war'
            }
           
        }
        stage("Deploy on Prod"){
            steps{
                // deploy on container -> plugin 
                deploy adapters: [tomcat9(credentialsId: 'tomcatServerDetails', path: '', url: 'http://44.204.44.210:8081')], contextPath: '/app', war: '**/*war'
            }
           
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
