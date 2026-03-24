Privvy is a project designed for EUC admins who run into legacy apps that need priviledge elevation, but don't have the tools such as DEM or Ivanti to allow for it. Much like these products, we can specify which processes
are allowed to be elevated, including file path, hash, publisher information, etc. Privvy requires .NET 8.0+ runtime on the client machine. 

*** Install instructions ***

Extract privvy-installer contents and navigate to the directory. Run privvy.service.exe --install --config-source config.sample.json

The example config file allows for C:\Windows\System32\notepad.exe to be elevated so you can test. Modify as needed. 

The install places the required files within C:\Program Files\Privvy and the configuration json and logs within C:\Programdata\Privvy. It also modifies the ACL so that only administrators and SYSTEM are able to view the
contents. It also creates a service called Privvy that runs under SYSTEM context to allow for the elevation to occur. To re-read the config JSON, simply restart the service. 

To test the elevation with the default JSON, run C:\Program Files\Privvy\privvy.stub.exe --target C:\Windows\System32\notepad.exe as a normal user. You'll notice that notepad is executed as elevated.

If the app requested does not line up with the ruleset, the launch from the privvy.stub.exe is denied. 

This tool can obviously be abused, so use only on the applications that absolutely require it and cannot spawn child processes. Use at your own risk. 
