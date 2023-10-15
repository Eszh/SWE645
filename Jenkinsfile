pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = credentials ('dockerpass')
	}
	stages{
		stage("Building the Student Survey Image"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf Swe-645-Assignment2.war *'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh 'docker login -u eeshwar4116 -p ${DOCKERHUB_PASS}'
					sh 'docker build -t eeshwar4116/surveypage .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push eeshwar4116/surveypage'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
					sh 'kubectl rollout restart deploy deployment -n assignmentnamespace'
				}
			}
		}
	}
}
