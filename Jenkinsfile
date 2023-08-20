pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'b9c4f564-54e0-4d36-b0bb-74a2a57eb2ca', path: '', url: 'http://172.31.38.97:8080')], contextPath: 'testapp1', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'b9c4f564-54e0-4d36-b0bb-74a2a57eb2ca', path: '', url: 'http://172.31.47.49:8080')], contextPath: 'prodapp1', war: '**/*.war'
            }
        }
    }
}
