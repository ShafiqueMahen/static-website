pipeline {
   agent any
   stages {
    //   stage('Install AWS S3 Upload Plugin') {
    //      steps {
    //          echo "Installing AWS SDK..."
    //         script {
    //           def plugin = Jenkins.instance.getPluginManager().getPlugin('s3')
    //           if (plugin == null) {
    //               Jenkins.instance.getPluginManager().installPlugin('s3')
    //               Jenkins.instance.restart()
    //           }
    //         }
    //      }
    //   }
      stage('Clone GitHub Repo') {
         steps {
            echo "Cloning repo..."
            git branch: "main",
            url: 'https://github.com/ShafiqueMahen/static-website.git'
            sh 'ls'
         }
      }
      stage('Build Website') {
         steps {
            echo "Building website..."
            dir('static-website/WebsiteProject') {
               sh 'npm install'
               sh 'npm run build'
            }
         }
      }
      stage('Deploy to S3') {
         steps {
             echo "Deploying to S3..."
            withAWS(region: 'eu-west-2', credentials: '43ba8cdb-ef00-49ce-8e01-d3e3fc8fd06c') {
               s3Upload(bucket: 'too-many-cooks-website', workingDir: 'dist', includePathPattern: '**/*')
            }
         }
      }
   }
}
