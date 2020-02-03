def FAILED_STAGE
podTemplate(cloud:'openshift',label: 'dotnet',
  containers: [
    containerTemplate(
      name: 'jnlp',
      image: 'blrocpimpregistry:5000/manya97/jnlp-slave-dotnet:slave',
      alwaysPullImage: true,
      privileged: true,
      envVars: [envVar(key:'http_proxy',value:''),envVar(key:'https_proxy',value:'')],
      args: '${computer.jnlpmac} ${computer.name}',
      ttyEnabled: true
    )])
{
node('dotnet') 
{
   stage('Checkout')
   {
       git credentialsId: 'userId', url: 'https://github.com/manyatripathi/SampleCliApp', branch: 'master'
       
   }
   
   stage('Initial Setup')
   {
	FAILED_STAGE=env.STAGE_NAME
	sh 'setx http_proxy http://gaurav.walecha:Infosys2203@10.68.248.34:80'
	sh 'setx https_proxy http://gaurav.walecha:Infosys2203@10.68.248.34:80'
	sh 'dotnet --version'
        sh 'dotnet restore --configfile nuget.config'
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
