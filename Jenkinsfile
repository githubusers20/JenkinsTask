node {
    properties([parameters([string(defaultValue: 'ronaldo', description: '', name: 'name', trim: false)])])
   def mvnHome
   stage('Preparation') { // for display purposes
     checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/githubusers20/JenkinsTask.git']]])
           
      mvnHome = tool 'maven1'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Post Job'){
       sh 'bin/makeindex'
   }
   stage('Results') {
      archiveArtifacts 'index.jsp'
   }
}
