node {
 try {
  
  stage('Preparation') {
    git 'https://github.com/swetamankar/CICD_jenkins.git'
   mvnHome = tool 'maven'
  }

try {
  stage('Deploy to Test') {
   // Run the maven build
   sh "mvn -f $WORKSPACE/proxies/pom.xml install -Ptest -Dorg=swetamankar-eval -Dusername=sweta.mankar@fiserv.com -Dpassword=Noida@123 -Dapigee.config.options=update -X validate"
   cucumber fileIncludePattern: '**/proxies/payment-v2/target/reports.json', sortingMethod: 'ALPHABETICAL'
   }
}catch (e) {
   //if tests fail, we can use a shell script which has 3 APIs to undeploy, delete current revision & deploy previous revision
   //sh "$WORKSPACE/undeploy.sh"
   throw e
  } finally {
   
  }
  
try {
  stage('Deploy to Production') {
   // Run the maven build
   sh "mvn -f $WORKSPACE/proxies/pom.xml install -Pprod -Dorg=swetamankar-eval -Dusername=sweta.mankar@fiserv.com -Dpassword=Noida@123 -Dapigee.config.options=update -X validate"
  }
  } catch (e) {
   //if tests fail, we can use a shell script which has 3 APIs to undeploy, delete current revision & deploy previous revision
   //sh "$WORKSPACE/undeploy.sh"
   throw e
  } finally {
   
  }
 } catch (e) {
  currentBuild.result = 'FAILURE'
  throw e
 } finally {
  
 }
}

