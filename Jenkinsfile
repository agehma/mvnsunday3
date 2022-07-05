pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/mvnsunday3.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'first download failed', cc: '', from: '', replyTo: '', subject: 'git failed', to: 'tg@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build artifact', cc: '', from: '', replyTo: '', subject: 'mvn failed', to: 'devt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '3933de1f-781a-4384-bab7-5258db7fbfd3', path: '', url: 'http://172.31.85.178:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'tomcat failed to deploy to qa server', cc: '', from: '', replyTo: '', subject: 'deploy failed', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

