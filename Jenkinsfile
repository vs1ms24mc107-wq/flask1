pipeline
{
	agent any
	environment
	{
		DOCKER_CREDENTIALS=credentials('dh1')
		Image_Name="vs1ms24mc107/my_webapp"
	}
	stages
	{
		stage('checkout')
		{
			steps
			{
				git branch:"main", url:"https://github.com/vs1ms24mc107-wq/flask1.git"
			}
		}
		stage('Build docker image')
		{
			steps
			{
				script{
					dockerImage=docker.build("${Image_Name}:latest")
				}
			}
		}
		stage('push to docker hub')
		{
			steps
			{
				script
				{
					docker.withRegistry("https://index.docker.io/v1/","dh1")
					{
						dockerImage.push()
					}
				}
			}
		}
	}
	post
	{
		success
		{
			echo "pipeline successful"
		}
		failure
		{
			echo "pipeline failed"
		}
		always
		{
			echo "cleaning up workspace"
			deleteDir()
		}
	}
}
