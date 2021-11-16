pipeline
{
    agent any
    stages
    {
        stage('Continuous Download')
        {
            steps
            {
                script
                {
                    try
                      {
                         git 'https://github.com/golu-24/Maven.git'
                      }
                    catch (Exception e1)
                      {
                        mail bcc: '', body: 'Git Has failed to download the file', cc: '', from: '', replyTo: '', subject: 'Git Download Failed', to: 'Dev@gmail.com'
                        exit(1)
                      }
                }
                
            }
        }    
            
             stage('Continuous Build')
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
                        mail bcc: '', body: 'Git Has failed to build the file', cc: '', from: '', replyTo: '', subject: 'Build  Failed', to: 'Dev@gmail.com'
                        exit(1)
                      }
                }
                
            }
        }
         stage('Continuous Deployment')
        {
            steps
            {
                
             script
                {
                    try
                      {
                         deploy adapters: [tomcat9(credentialsId: '2603d993-e8aa-4b8e-8474-58f6f21e4472', path: '', url: 'http://172.31.25.117:8080')], contextPath: 'T1', war: '**/*.war'
                      }
                    catch (Exception e3)
                      {
                        mail bcc: '', body: 'Deployment  Has failed ', cc: '', from: '', replyTo: '', subject: 'Git Download Failed', to: 'Dev@gmail.com'
                        exit(1)
                      }
                }
            }  
        }
            stage('Continuous Testing')
        {
            steps
            {
                script
                {
                    try
                      {
                         git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                         sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                
                      }
                    catch (Exception e4)
                      {
                        mail bcc: '', body: 'Testing   Has failed ', cc: '', from: '', replyTo: '', subject: 'testing Failed', to: 'Test@gmail.com'
                        exit(1)
                      }
                }
            }  
        }
               
         stage('Continuous Delivery')
        {
            steps
            {
                 script
                {
                    try
                      {
                          deploy adapters: [tomcat9(credentialsId: '2603d993-e8aa-4b8e-8474-58f6f21e4472', path: '', url: 'http://172.31.25.117:8080')], contextPath: 'T1', war: '**/*.war'
                                                }
                    catch (Exception e5)
                      {
                        mail bcc: '', body: 'Testing   Has failed ', cc: '', from: '', replyTo: '', subject: 'testing Failed', to: 'Test@gmail.com'
                        exit(1)
                      }
                }
               
            }
        }
    }    
}
