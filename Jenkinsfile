node {
deleteDir()
  checkout scm
  def workspace = pwd()
  
  
  script {
  if (env.BRANCH_NAME == '*mas') {
    stage ('Some Stage 1 for master') {
	echo "**************DID CHANGES TO MASTER BRANCH ****************"
        def server = Artifactory.server 'central'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        //def javaHome = tool name: 'java1.8', type: 'hudson.model.JDK'
        //def mvnHome = tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
	rtMaven.tool = 'maven3'
        
        timestamps {
             
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
          
                }
                 // Mark the code checkout 'stage'....
                stage ('Checkout') {
                   // Checkout code from repository
                   checkout scm
				  // git ([url: 'ssh://git@stash.agilysys.local:7999/mblp/mobilepaymentinterface.git', branch: 'master'])


                 }

                stage('Artifactory configuration') {
                    rtMaven.tool = 'maven3'
                    rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
                   // rtMaven.resolver releaseRepo: 'repo', snapshotRepo: 'repo', server: server
                    buildInfo = Artifactory.newBuildInfo()
                    rtMaven.deployer.deployArtifacts = true // Disable artifacts deployment to artifactory
                }
                stage('mvn goals execution') {
                    rtMaven.run pom: 'pom.xml', goals: 'clean install'
		    
		 }
            
        }
    }
    }


  
  
  
  
  
  

  
  else if (env.BRANCH_NAME == 'dev*') {
    stage ('Some stage branch step') {
      def server = Artifactory.server 'central'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        //def javaHome = tool name: 'java1.8', type: 'hudson.model.JDK'
        //def mvnHome = tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
	rtMaven.tool = 'maven3'
        
        timestamps {
             
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
					echo "*****************ITS DEV* JOB WORKING ON DEVELOP BRANCH"
          
                }
                 // Mark the code checkout 'stage'....
                stage ('Checkout') {
                   // Checkout code from repository
                   checkout scm
				   // git ([url: 'ssh://git@stash.agilysys.local:7999/mblp/mobilepaymentinterface.git', branch: 'develop'])
                 }

                stage('Artifactory configuration') {
                    rtMaven.tool = 'maven3'
                    rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
                   // rtMaven.resolver releaseRepo: 'repo', snapshotRepo: 'repo', server: server
                    buildInfo = Artifactory.newBuildInfo()
                    rtMaven.deployer.deployArtifacts = true // Disable artifacts deployment to artifactory
                }
                stage('mvn goals execution') {
                    rtMaven.run pom: 'pom.xml', goals: 'clean install'
		    
		 }
            
        }
    }
    }
	
    



  else {
    sh 'echo "Branch not applicable to Jenkins... do nothing"'
  }
 
}
}

