pipeline{	
		 agent { label 'master' }
	
		 stages
				{
					stage("Git Checkout")
						{
						 steps
								{
								 git branch: 'Branch-5', url: 'https://github.com/prashanth-konakala-bluepal/Multi-Branch-Pipeline.git'
								}
						}
					stage("Maven Build")
						{
						 steps
								{
								 sh "mvn clean package"
								 sh "mv /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-5/webapp/target/*.war /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-5/webapp/target/Branch-5.war"
								}
						}		
					stage("Deploying to Dev")
						{
						 steps
								{
								 sshagent(['Tomcat_server-1'])
										{
										 sh """
										
											scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Multi-Branch-Pipeline_Branch-5/webapp/target/Branch-5.war ubuntu@3.15.198.149:/opt/tomcat/webapps/
																					
										"""
										}
								}
						}
				}	
		}
