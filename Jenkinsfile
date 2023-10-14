pipeline {
       agent any
       environment {
        DOCKERHUB_PASS = credentials ('docker-pass')

}
stages {
           stage("Building the Student Survey Image") {
           steps
              script {
                checkout scm
                sh 'rm -rf *.war'
                sh 'jar -cvf Swe-645-Assignment2.war -C WebContent/ .'
                sh 'echo ${BUILD_TIMESTAMP}'
                sh "docker login -u eeshwar4116 -p ${DOCKERHUB_PASS}"
                def customImage = docker.build("eeshwar4116/surveypage:${BUILD_TIMESTAMP}")
}

}
stage("Pushing Image to DockerHub") {
steps {
script {
sh 'docker push eeshwar4116/surveypage:${BUILD_TIMESTAMP}'
}
}
}
stage("Deploying to Rancher as single pod") {
    steps {
        sh 'kubectl set image deployment/stusurvey-pipeline stusurvey-pipeline-eeshwar4116/surveypage:${BUILD_TIMESTAMP} -n jenkins-pipeline'

}
}
stage("Deploying to Rancher as with load balancer") {
steps {
    sh 'kubectl set image deployment/surveypage-lb surveypage-lb-eeshwar4116/surveypage:${BUILD_TIMESTAMP} -n jenkins-pipeline'
}
}
}
}
