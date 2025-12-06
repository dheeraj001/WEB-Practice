pipeline {
    agent any

    stages {
        stage('Create a web directory') {
        
            input {
              message 'Enter the data'
              parameters {
                    string defaultValue: 'dheeraj', description: 'Author of web development application', name: 'Author'
                    string defaultValue: 'dev', description: 'Env which you want o run ', name: 'env'
              }
            }
            steps{
                echo "The responsible of this project is ${Author}  and will be deployed in ${env}"
                // First drop the directory if its exist
                sh 'rm -rf /var/lib/jenkins/web '
                // Create the directory 
                sh 'mkdir -p /var/lib/jenkins/web'
            }
        }
        stage('Drop the Apache HTTPD container'){
            steps{
                echo 'dropping the container'
                sh 'docker rm -f apache1'
            }
        }
        stage('Creating the Apache httpd container'){
            steps{
                echo 'Creating the Container'
                sh 'docker run -dit --name apache1 -p 9000:80  -v /var/lib/jenkins/web:/usr/local/apache2/htdocs/ httpd'
            }
        }
        stage('Copy the web application to container directory'){
          steps{
            sh 'cp -r web/* /var/lib/jenkins/web'
          }
        } 
        stage('Checking the app'){
            steps{
                sh 'wget http://192.168.29.48:9000'
            }
        }
    }        
}
