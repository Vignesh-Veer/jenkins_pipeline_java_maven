node {
   // Mark the code checkout 'stage'....
   stage 'Checkout'
   
   git url: 'https://github.com/Vignesh-Veer/jenkins_pipeline_java_maven.git'

   // Get the maven tool.
   // ** NOTE: This 'M3' maven tool must be configured
   // **       in the global configuration.           
   def mvnHome = tool 'M3'

   // Mark the code build 'stage'....
   stage 'Build'
   // Run the maven build
   sh "${mvnHome}/bin/mvn -Dmaven.test.failure.ignore clean package"
   step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
//}

/*node {
 
  notifyStarted()
 
  /* ... existing build steps ... */
//}
 
/*def notifyStarted() {
  // send to email
  emailext (
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
      //recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )
}*/


/*stage 'Test'
node {
    try {
        sh 'exit 1'
    } finally {
        println currentBuild.result  // this prints null
        step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'priyasapo@gmail.com', sendToIndividuals: true])
    }
}

stage 'Test'
node {
    try {
        sh 'exit 1'
        currentBuild.result = 'SUCCESS'
    } catch (any) {
        currentBuild.result = 'FAILURE'
        throw any //rethrow exception to prevent the build from proceeding
    } finally {
        step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'priyasapo@gmail.com', sendToIndividuals: true])
    }
}

stage 'Test'
node {
    catchError {
        sh 'exit 1'
    } 
    step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'priyasapo@gmail.com', sendToIndividuals: true])
}
*/

//node {
   try {
     notifyStarted()
 
     / ... existing build steps ... /
 
     notifySuccessful()
   } catch (e) {
     currentBuild.result = "FAILED"
     notifyFailed()
     throw e
   }
 }
 
 def notifyStarted() { / .. / }
 
 def notifySuccessful() { / .. / }
def notifyFailed() {
 
   emailext (
       subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
       body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
         <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>""",
       recipientProviders: [[$class: 'DevelopersRecipientProvider']]
     )
 }
