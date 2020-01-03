 pipeline {
   agent any-with-jdk8-maven-curl-unzip
   stages {
   stage('Maven Build') {
   steps {
   - sh 'maven clean verify'
   }
   }
   stage('Veracode DevOps Scan') {
   steps {
   - sh `curl -O https://downloads.veracode.com/securityscan/devops-
scanner-java-LATEST.zip`
   - sh `unzip devops-scanner-java-LATEST.zip devops-scanner-java.jar`
   - sh `java -jar devops-scanner-java.jar \
   --api_id "${8cffaa8bf72c9455b43ff8a5ac034d07}" \
   --api_secret_key "${1f9330e9f3a8ab55624c97ab4c8c9483f061fce18678297dea712d50b85f5925704cbb06b59e61bc6f67407205cffe2422a55640acb0a8d0a141dbef964b18c6}" \
   --project_name "${env.JOB_NAME}" \
   --project_url "${env.GIT_URL}" \
   --project_ref "${env.GIT_COMMIT}" \
   }
   }
   }
   post {
   always {
   archiveArtifacts artifacts: 'results.json', fingerprint: true
   }
   }
   }
