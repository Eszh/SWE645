pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = 'Justdoit4uu@'
	}
	stages{
		stage("Building the Student Survey Image"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf Swe645Assignment2.war -C /var/lib/jenkins/workspace/Swe645-Assignment2 .'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh 'docker login -u eeshwar4116 -p ${DOCKERHUB_PASS}'
					sh 'docker build -t eeshwar4116/swe645survey:$BUILD_TIMESTAMP .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push eeshwar4116/swe645survey:$BUILD_TIMESTAMP'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
					 // sh 'kubectl set image  deployment/swedeployment container-0=eeshwar4116/swe645survey:$BUILD_TIMESTAMP'
                                     sh 'kubectl rollout restart deploy swedeployment'

				}
			}
		}
	}
}
