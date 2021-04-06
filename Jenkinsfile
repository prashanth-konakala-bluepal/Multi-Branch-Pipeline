pipeline{		 
		 agent any
		 
		 environment
			 {
			  PATH = "/opt/apache-maven-3.6.3/bin:$PATH"
			 }
		 
			 {
			  PATH = "/opt/jdk-11.0.10/bin:$PATH"
			 }
		 stages
				{
					stage("Git Checkout")
						{
						 steps
								{
								 git branch: 'main', url: 'https://github.com/prashanth-konakala-bluepal/Multi-Branch-Pipeline.git'
								}
						}
					stage("Maven Build")
						{
						 steps
								{
								 sh "mvn clean package"
								 sh "mv /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-2/webapp/target/*.war /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-2/webapp/target/Branch-2.war"
								}
						}		
					stage("Deploying to Dev")
						{
						 steps
								{
								 sshagent(['Tomcat_server-1'])
										{
										 sh """
										
											scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-2/webapp/target/Branch-2.war ubuntu@3.17.175.98:/opt/tomcat/webapps/
											
											ssh ubuntu@3.17.175.98 /opt/tomcat/bin/shutdown.sh
											
											ssh ubuntu@3.17.175.98 /opt/tomcat/bin/startup.sh
											
										"""
										}
								}
						}
				}	
		}
