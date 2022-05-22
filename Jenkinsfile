node('master') 
{
  stage('ContinousDownload')
  {
      try
      {
          git 'https://github.com/rbngtm1/CI_CD_Integration.git'
      }
      catch(Exception e1)
      {
          mail bcc: '', body: 'Hello Developers, Jenkins failed to download the code. Please verify', cc: '', from: '', replyTo: '', subject: 'Code failed to download', to: 'ewambe5@gmail.com'
          exit(1)
      }
  }
  stage('ContinousBuild')
  {
      try
      {
          sh 'mvn package'
      }
      catch(Exception e2)
      {
          mail bcc: '', body: 'code failed to build aritifact', cc: '', from: '', replyTo: '', subject: 'failed to build artificat', to: 'ewambe5@gmail.com'
          exit(1)
      }
  }
   stage('ContinousDeployment')
  {
      try
      {
          deploy adapters: [tomcat9(credentialsId: '2357967a-6703-423f-87f7-30a1ec349d35', path: '', url: 'http://172.31.6.114:8080')], contextPath: 'testapp', war: '**/*.war'
      }
      catch(Exception e3)
      {
          mail bcc: '', body: 'artifact failed to deploy', cc: '', from: '', replyTo: '', subject: 'failed to deploy to qa server', to: 'ewambe5@gmail.com'
          exit(1)
      }
  } 
   stage('ContinousTesting')
  {
      try
      {
          git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
          sh 'java -jar /home/ubuntu/.jenkins/workspace/Scriptedpipeline/testing.jar'
      }
      catch(Exception e4)
      {
          mail bcc: '', body: 'failed to download code', cc: '', from: '', replyTo: '', subject: 'failed to download', to: 'ewambe5@gmail.com'
          exit(1)
      }
  } 
   stage('ContinousDelivery')
  {
      try
      {
          deploy adapters: [tomcat9(credentialsId: '2357967a-6703-423f-87f7-30a1ec349d35', path: '', url: 'http://172.31.11.156:8080')], contextPath: 'prodapp', war: '**/*.war'
      }
      catch(Exception e5)
      {
          mail bcc: '', body: 'failed to deploy to prod server', cc: '', from: '', replyTo: '', subject: 'please fix', to: 'ewambe5@gmail.com'
          exit(1)
      }
  } 
}
