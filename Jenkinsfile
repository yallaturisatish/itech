pipeline
{
    agent any
    stages
    {
        stage("Continues download")
        {
            steps
            {
                git branch: 'main', url: 'https://github.com/yallaturisatish/itech.git'
            }
        }
        stage("Continues Build")
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage("Continues deploy")
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '7f90c3d6-00d4-4ccf-82d6-92b5cc7aedec', path: '', url: 'http://172.31.66.212:8080')], contextPath: 'pipeline-qa-env', war: '**/*.war'
            }
        }
        stage("Continues testing")
        {
            steps
            {
                git branch: 'master', url: 'https://github.com/yallaturisatish/Testing.git'
                sh 'java -jar /var/lib/jenkins/workspace/dev-scripted-pipeline/testing.jar'

            }
        }
        stage("Continues delivery")
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'b367fcb7-e870-4620-b7da-f2d4a900ce8d', path: '', url: 'http://172.31.3.73:8080')], contextPath: 'pipeline-prod-env', war: '**/*.war'
            }
        }
    }
}    
