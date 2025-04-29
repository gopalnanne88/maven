pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage(ContBuild)
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '0bfa7b57-b843-414b-8643-74cdfd56e637', path: '', url: 'http://172.31.11.63:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DP1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                input message: 'Need Approval', submitter: 'reyansh'
                deploy adapters: [tomcat9(credentialsId: '0bfa7b57-b843-414b-8643-74cdfd56e637', path: '', url: 'http://172.31.3.35:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
