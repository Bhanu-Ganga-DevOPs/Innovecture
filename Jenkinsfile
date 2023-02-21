pipeline {
    agent any
    
    tools{
    maven 'Apache_Maven_3.6.3'
    
    }
    
    stages {
        stage('Code-checout') {
            steps {
                git branch: 'main', credentialsId: '49014944-2d3e-44be-a5dc-c8c970b21d61', url: 'https://github.com/Bhanu-Ganga-DevOPs/Innovecture.git'
            }
        }
       stage('Maven-build'){
            steps{
                
                    sh "mvn clean package"
                    sh "mv target/*.war target/myweb.war"
                
                
                
            }
        }
        
        stage('Deploy to Apacheserver'){
            steps{
              sshagent(["tomcat-new"]) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war ubuntu@172.31.46.103:/home/ubuntu/apache-tomcat-9.0.71/webapps/
                    ssh ubuntu@172.31.46.103 /home/ubuntu/apache-tomcat-9.0.71/bin/shutdown.sh
                    ssh ubuntu@172.31.46.103 /home/ubuntu/apache-tomcat-9.0.71/bin/startup.sh
                """
              }
            }
    }
}
