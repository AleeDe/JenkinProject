pipeline{
    agent any
    tools {
        maven 'Maven' 
    }
    stages{
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                echo "========Test========"
            } 
        }
        stage("Build"){
            steps{
                sh "mvn package"
                echo "========Build========"
            } 
        }
        stage("Deploy-Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'pipeline', path: '', url: 'http://43.205.135.20:8080')], contextPath: '/app', war: '**/*war'
                echo "========Deploy-Test========"
            } 
        }
        stage("Deploy-Prod"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'pipeline', path: '', url: 'http://13.233.13.246:8080')], contextPath: '/app', war: '**/*war'
                echo "========Deploy-Prod========"
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