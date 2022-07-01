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
                 //slackSend channel: 'rk', message: 'Job Started'
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
                deploy adapters: [tomcat9(credentialsId: 'desc1', path: '', url: 'http://3.80.84.137:8081/')], contextPath: '/app', war: '**/*war'
            }
           
        }
        stage("Deploy on Prod"){
            //this is for manual approval ->deploy for prod "no direct deployment"
            input {
                message "Should we continue?"
                ok "Yes we Should"
            }
            steps{
                // deploy on container -> plugin 
                deploy adapters: [tomcat9(credentialsId: 'desc1', path: '', url: 'http://54.221.60.140:8081')], contextPath: '/app', war: '**/*war'
            }
           
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
            //slackSend channel: 'rk', message: 'Success'
        }
        failure{
            echo "========pipeline execution failed========"
             //slackSend channel: 'rk', message: 'Job Failed'
        }
    }
}
