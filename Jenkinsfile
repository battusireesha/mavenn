pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
              deploy adapters: [tomcat9(credentialsId: '2b1bbd71-ab48-40c2-8bab-b636aef80982', path: '', url: 'http://172.31.33.117:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
               

            }
        }
        stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '2b1bbd71-ab48-40c2-8bab-b636aef80982', path: '', url: 'http://172.31.36.161:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
            
        }
    }
}



