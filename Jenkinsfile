pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Security Scan') {
              steps {  
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1',outputFormat: 'json', onDisallowed: 'fail'
              }
         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-1', credentials:'aws-static') {
                    // do something
                    s3Upload(bucket:"jenkins-pipelines-on-aws", includePathPattern:'**/*');
                }
              }
         }
     }
}
