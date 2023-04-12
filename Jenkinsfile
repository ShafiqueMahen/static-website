pipeline {
   agent any
   stages {
      stage('Clone GitHub Repo') {
         steps {
            echo "Cloning repo..."
            git branch: "main",
            url: 'https://github.com/ShafiqueMahen/static-website.git'
            sh 'ls'
         }
      }
      stage('Deploy to S3') {
         steps {
             echo "Deploying to S3..."
            withAWS(region: 'eu-west-2', credentials: '43ba8cdb-ef00-49ce-8e01-d3e3fc8fd06c') {
               s3Upload(bucket: 'too-many-cooks-website', workingDir: '', includePathPattern: '**/*')
            }
         }
      }
   }
}
