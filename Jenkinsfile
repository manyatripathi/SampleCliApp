def FAILED_STAGE
podTemplate(cloud:'openshift',label: 'dotnet',
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'blrocpimpregistry:5000/manya97/jnlp-slave-dotnet:latest',
      alwaysPullImage: true,
      privileged: true,
      envVars: [envVar(key:'http_proxy',value:''),envVar(key:'https_proxy',value:'')],
      args: '${computer.jnlpmac} ${computer.name}',
      ttyEnabled: true
    )])
{
node('dotnet') 
{
   def MAVEN_HOME = tool "Maven_HOME"
   def JAVA_HOME = tool "JAVA_HOME"
   env.PATH="${env.PATH}:${MAVEN_HOME}/bin:${JAVA_HOME}/bin"
   stage('Checkout')
   {
       git credentialsId: 'userId', url: 'https://github.com/manyatripathi/SampleCliApp', branch: 'master'
       
   }
   
   stage('Initial Setup')
   {
		FAILED_STAGE=env.STAGE_NAME
       sh 'dotnet restore --configfile NuGet.Config'
	   sh 'dotnet clean'
   }
   
    stage('Build and Pack')
   {
        FAILED_STAGE=env.STAGE_NAME
        sh 'dotnet build --configuration Release'
		sh 'dotnet pack --no-build --output nupkgs'
   }
  
	     
}
}
