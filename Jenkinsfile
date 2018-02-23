    node('STAY_NODES') {
        def server = Artifactory.server '-1946595677@1447381539347'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        def javaHome = tool name: 'JDK 1.8', type: 'hudson.model.JDK'
        def mvnHome = tool name: 'Maven 3', type: 'hudson.tasks.Maven$MavenInstallation'
        
        timestamps {
            ansiColor('xterm') {
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
          
                }
                 // Mark the code checkout 'stage'....

  checkout scm
  def workspace = pwd()

  if (env.BRANCH_NAME == 'master') {
    echo "*******************this is MASTER ***************"
    
	                     stage('Artifactory configuration') {
                    rtMaven.tool = 'Maven 3.3.9'
                    rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
                    rtMaven.resolver releaseRepo: 'repo', snapshotRepo: 'repo', server: server
                    buildInfo = Artifactory.newBuildInfo()
                    rtMaven.deployer.deployArtifacts = false // Enabling artifacts deployment to artifactory
                }
                stage('mvn goals execution') {
                    rtMaven.run pom: 'pom.xml', goals: 'clean install -Darguments=maven.repo.local=$WORKSPACE/.m2/repository'
    //  sh 'do something'


  }

  else if (env.BRANCH_NAME == 'branch1') {
    node {
        def server = Artifactory.server 'central'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        //def javaHome = tool name: 'java1.8', type: 'hudson.model.JDK'
        //def mvnHome = tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
	rtMaven.tool = 'maven3'
        
        timestamps {
             
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
			echo "*************BRANCH1***********************"
          
                }
                 // Mark the code checkout 'stage'....
                stage ('Checkout') {
                   // Checkout code from repository
                   checkout scm
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
  
  else if (env.BRANCH_NAME == 'branch1') {
  node {
        def server = Artifactory.server 'central'
        def rtMaven = Artifactory.newMavenBuild()
        def buildInfo
        
        //def javaHome = tool name: 'java1.8', type: 'hudson.model.JDK'
        //def mvnHome = tool name: 'maven3', type: 'hudson.tasks.Maven$MavenInstallation'
	rtMaven.tool = 'maven3'
        
        timestamps {
             
                stage("Initialize Build") {
                    echo "EXECUTING ON THE NODE: $env.NODE_NAME"
			echo " ********************this id branch BRANCH2 ************************"
          
                }
                 // Mark the code checkout 'stage'....
                stage ('Checkout') {
                   // Checkout code from repository
                   checkout scm
                 }

                stage('Artifactory configuration') {
                    rtMaven.tool = 'maven3'
                    rtMaven.deployer releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local', server: server
                   //nnnnn rtMaven.resolver releaseRepo: 'repo', snapshotRepo: 'repo', server: server
                    buildInfo = Artifactory.newBuildInfo()
                    rtMaven.deployer.deployArtifacts = true // Disable artifacts deployment to artifactory
                }
                stage('mvn goals execution') {
                    rtMaven.run pom: 'pom.xml', goals: ' release:clean release:prepare release:perform'
		    
		 }
            
        }
    }
  }

  else {
    sh 'echo "Branch not applicable to Jenkins... do nothing"'
  }
}