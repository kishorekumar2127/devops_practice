pipeline	{
	agent	any;
	stages	{
		stage('Preparing the environment')	{
			steps	{
				sh	'python3 -m pip install -r requirements.txt'
			}
		}
		stage('Code	Quality')	{
			steps	{
				sh	'python3 -m pylint app.py'
			}
		}
		stage('Tests')	{
			steps	{
				sh	'python3 -m pytest'
			}
		}
		stage('Build')	{
			agent {
				node {
					label "DockerServer";
				}
			}
			steps {
				sh 'docker build -f https://github.com/kishorekumar2127/devops_practice.git devops_practice:latest'
			}
		}
	
		stage('Deploy')	{
			agent	{
				node{
					label "DockerServer";
				}
			}
		
		
			steps {
				sh 'docker	run	-tdi	-p	5000:5000	kishorekumar2127:latest'
			}
		}
	}
}