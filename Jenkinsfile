def FAILED_STAGEs
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
   withEnv(['http_proxy=http://gaurav.walecha:Infosys2203@10.74.91.103:80','https_proxy=http://gaurav.walecha:Infosys2203@10.74.91.103:80']) 
{
   stage('Initial Setup')
   {
	FAILED_STAGE=env.STAGE_NAME
	sh 'printenv | grep http'
	print env.http_proxy
	sh 'dotnet --version'
        sh 'dotnet restore'
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
}
