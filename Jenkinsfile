
 
 pipeline {
    agent any
	 enviroment {
	 path= "/opt/maven3/bin:$path"
	 }
	 
	  stages {
        stage("Git checkout") {
		
		  git credentiaIsId: 'javahome2', url: 'https://github.com/murthy11/myweb-repo.git'
		  
		  }
		 }
 
      
        stage('Maven Build') {
           
            steps {
             
                sh 'mvn clean package'
				sh " mv target/*.war target/myweb-repo.war
            }
        }
        stage('deploy-dev') {
            
            steps {
			  sshagent([tomcat-new]) {
               sh"""
			   scp -o Stricthostkeychecking=no target/myweb.war ec2-user@44.193.219.207:/root/apache-tomcat-9.0.62/webapps
			   
			   ssh ec2-user@44.193.219.207/root/apache-tomcat-9.0.62/bin/shutdown.sh
			   
			   
			   """
			   
			   }
			   
			   
            }
        }
    }

