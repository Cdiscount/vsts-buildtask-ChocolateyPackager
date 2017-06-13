This extension allow you to create a [Chocolatey](https://chocolatey.org) package (*.nupkg*) and publish it to a repository.

This extension can launch the following commands :
 - `choco pack` ([doc](https://chocolatey.org/docs/commands-pack))
 - `choco  push` ([doc](https://chocolatey.org/docs/commands-push))

___

## How its work

1. Add this task into a build or release with a bulid artifact that contains a *.nuspec* file
1. Set the parameters :
   * The drop folder path : RelativePath that contains the *.nuspec* file 
	   * Ex: `$(System.DefaultWorkingDirectory)\MyChocolateyApplication`
   * Name of the nuspec file 
	   * Ex: `MyChocolateyApplication.nuspec`
   * The chocolatey reposiroty url 
	   * Ex: `https://chocolateyrepo.domain.com/repository/chocolatey`
   * Chocolatey user api key : You can add a *secret* variable (Ex: ApiKey) in *Configuration* tab and call it 
	   * Ex: `$(ApiKey)`
   * Use Force option : launch `choco push` with `--force` parameter. 
	   * Use it if the repo is not https procotol ([doc](https://chocolatey.org/docs/commands-push))
   * Pack only : pack the chocolatey package, but don't push it. 
	   * The *.nupkg* file is available in the build/release drop folder
   
1. **Log example :** 
> 2017-05-05T09:21:44.9256244Z Starting ChocolateyPackAndPushTask
2017-05-05T09:21:44.9256244Z Location : D:\A01\_work\8ca771928\MyChocolateyApplication\drop
2017-05-05T09:21:44.9256244Z Attempting to pack .\MyChocolateyApplication.nuspec
2017-05-05T09:21:45.5975401Z Attempting to build package from 'MyChocolateyApplication.nuspec'.
2017-05-05T09:21:50.8635740Z Successfully created package 'MyChocolateyApplication.2.3.19.7.nupkg'
2017-05-05T09:21:50.9104523Z Attempting to push D:\A01\_work\8ca771928\MyChocolateyApplication\drop\MyChocolateyApplication.2.3.19.7.nupkg to source https://nuget.myrepository.com/Chocolatey/
2017-05-05T09:21:50.9104523Z Launch command  D:\A01\_work\8ca771928\MyChocolateyApplication\drop\MyChocolateyApplication.2.3.19.7.nupkg -s https://nuget.myrepository.com/Chocolatey/ -k **********
2017-05-05T09:21:51.4104911Z Attempting to push MyChocolateyApplication.2.3.19.7.nupkg to https://nuget.myrepository.com/Chocolatey/
2017-05-05T09:21:54.9889260Z MyChocolateyApplication 2.3.19.7 was pushed successfully to https://nuget.myrepository.com/Chocolatey/
2017-05-05T09:21:54.9889260Z Your package may be subject to moderation. A moderator will review the
2017-05-05T09:21:54.9889260Z package prior to acceptance. You should have received an email. If you
2017-05-05T09:21:54.9889260Z don't hear back from moderators within 1-3 business days, please reply
2017-05-05T09:21:54.9889260Z to the email and ask for status or use contact site admins on the
2017-05-05T09:21:54.9889260Z package page to contact moderators.
2017-05-05T09:21:54.9889260Z Please ensure your registered email address is correct and emails from
2017-05-05T09:21:54.9889260Z chocolateywebadmin at googlegroups dot com are not being sent to your
2017-05-05T09:21:54.9889260Z spam/junk folder.
2017-05-05T09:21:55.0201449Z Ending ChocolateyPackAndPushTask

___

## Synchronize automatically *version* field

You have to change the ```<version>``` field each time you create a new version of your chocolatey package.
You can automatically synchronize your assembly version with this field by using another task available in the marketplace "*Nuget version synchronizer*". 
[Please find the extension here](https://marketplace.visualstudio.com/search?term=publisher:%22Cdiscount%20Alm%22&target=VSTS).

```xml
<?xml version="1.0"?>
<package>
  <metadata>
      <version>ASSEMBLY VERSION</version>
     ...
  </metadata>
  <files>
    ...
  </files>
</package>
```
___

## Enjoy!


Credits : Jean-Michel Michel, Alm Team, Cdiscount France.