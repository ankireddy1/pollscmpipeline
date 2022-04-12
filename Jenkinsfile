pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
            steps
            {
                git 'https://github.com/ankireddy1/pipe.git'
            }
        }
        stage('continuousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousdeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'a44d1769-4bc2-4fdb-81ba-11f0b546d493', path: '', url: 'http://172.31.32.65:8080')], contextPath: 'qaw', war: '**/*.war'
            }
        }
         stage('continuoustesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar testing.jar'
            }
        }
        stage('continuousdelivery')
        {
            steps
            {
                input message: 'required approval', submitter: 'anki'
                deploy adapters: [tomcat9(credentialsId: 'a44d1769-4bc2-4fdb-81ba-11f0b546d493', path: '', url: 'http://172.31.45.235:8080')], contextPath: 'pro', war: '**/*.war'
            }
        }
    }
}

