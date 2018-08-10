# Storebrowse for Receiver for Windows

Storebrowse is a command-line utility tool available with Receiver for Windows that you can use to customize Receiver by scripting the storebrowse utility. This version of Storebrowse (v1.0.1.44) utility is supported on Receiver for Windows Version 4.4 CU5, 4.7, 4.9, 4.9 CU1, 4.10, 4.10.1, 4.11 and 4.12.

Using Storebrowse utility, you can:

* Add a store
* Enumerate the desktops and apps from the configured store
* Launch the published Apps/Desktops from the configured store

**Note:**

* The current version of Storebrowse utility does not support NetScaler Gateway configuration.
* This utility is supported on StoreFront server only.


## Using the Storebrowse utility

Extract the Storebrowse.zip file downloaded from the Citrix downloads website to the desired location. The folder also contains dependent DLLs that are used along with Storebrowse.

Refer to the following table for information about the options that you can use from Storebrowse.

| Option | Description | Notes |
|---|---|---|
| `-a` | Adds new store. Execute the following command: <br> `storebrowse.exe –U <username> -P <password> -D <domain> -a <URL of Storefront>`| Returns the full URL of the store. If this fails, an error is reported. <br> **Note**: You can add multiple stores using the Storebrowse utility.<br> **Example**: `storebrowse.exe –U user123 –P password123 –D TestDomain –a https://my.secondexamplestore.net/Citrix/Store/discovery` |
| `-E`, `--enumerate` | Enumerates the available resources. Execute the following command:  <br> `storebrowse.exe –M 0X2000 –E or --enumerate <URL of Storefront>` | By default, the resource name, display name, and folder of the resource are displayed. Use the --details option to display additional information. <br> **Note**: The argument **-M 0X2000** is required to get the launch URL for each of the resource that are published in the Storefront <br> **Example**: `storebrowse.exe –M 0X2000 –E https://my.secondexamplestore.net/Citrix/Second/discovery` |
| `–q`, `--quicklaunch` | Specifies the name of the published resource to which you want to connect. Saves the required ICA file in the local folder where Storebrowse is running. Execute the following command: <br> `storebrowse.exe –quicklaunch <URL Of the Resource> <URL of the Storefront>` | **Note**: Executing the following command will save the ICA file in the local machine where the Storebrowse is running. The file will be saved under `%localAppData%\Citrix\storebrowse\cache` folder. <br> `Storebrowse.exe –quicklaunch <URL of the Resource> <URL of the Storefront>` <br> **Example**: `storebrowse.exe –q https://mysecondexamplestore.net/Citrix/Second/v2/v3jkjjlj9u0i0-/launch/ica  https://mysecondexamplestore.net/Citrix/Second/discovery` |
| `-L`, `--launch` | Launch an instance of the resource | Executing the following command saves the ICA file locally  where Storebrowse is running. The file is saved in the  %localAppData%\Citrix\storebrowse\cache folder. <br> `Storebrowse.exe –launch <Name of the Resource> <URL of the Storefront>` <br> In the above example, name of the App/Desktop is the name that is displayed while enumerating the resources from a particular Store Front. <br> After enumerating the resources using Storebrowse utility, the output will be displayed in the following format: `.\storebrowse –M 0X2000 –E https://mysecondexamplestore.net/Citrix/Second/discovery` results in the following output: <br> `'Controller.Calculator'	'Calculator'	'\'	''	http://abc-sf.xyz.com/Citrix/Stress/resources/v2/Q29udHJvbGxlci5DYWxjdWxhdG9y/launch/ica` <br> Use the first name that is displayed as an argument with –L  or –launch to generate the ICA file for a specific resource. `Storebrowse.exe –launch “Controller.Calculator”  https://mysecondexamplestore.net/Citrix/Second/discovery` |
| `-f`, `--launch file folder <folder path>` | Instead of creating ICA file, it will save the ICA file to the specified folder | Executing this command saves the ICA file to the user-defined destination instead of default location. However, this should  be used with the combination of –L command. <br> For example, `storebrowse –U <username” –P <userpassword> -D <Domain Name> –f C:\Test\test.ica  -L` |
| `-t`, `--traceauthentication` | Generates authentication trace file | Executing this command will generate Authmanager related logs, which will be used for further debugging/troubleshooting any authentication related issues. The logs will be generated at %localAppData%\Citrix\Storebrowse\logs <br> For example, `storebrowse –t –U <username> -P <UserPassword> -D <Domain_Name> -f “<Path_to_save_ICAfile> -L “Resource_Name” <Storefront_URL>` |
| `-d`, `--deletestore` | Unregisters a store with the Service Record daemon. Execute the following command: <br> `storebrowse.exe –d or –deletestore  <URL of Storefront>` | **Example**:  `storebrowse.exe –d http://store-url.xxx.com/Citrix/SF-Name/discovery` |
| `–S`, `–sessionlaunch` | You can actually launch the resource with the –S command line option. This option takes the following as parameters - Username, Password, Domain, Friendly name of the resource to be launched and the store URL. However, if the user does not provide the credentials , AuthManager prompt is thrown to enter the credentials and then the resource launch will happen. <br><br>`\storebrowse.exe  -U {Username} –P {Password} –D {Domain} –S “{Friendly_Resource_Name} <https://my.firstexamplestore.net/Citrix/Store/discovery` | Executing this command would generate the ICA file and then it would actually launch the session .<br><br>`.\storebrowse.exe –S {Published_App_Name} <URL of the Storefront server>`<br><br> For example, say if you have a published application by name Calculator which you actually intend to launch on the endpoint, then you can do so by running the below command:<br><br> `.\storebrowse –S “Calculator” https://my.firstexamplestore.net/Citrix/Store/discovery` |


## Limitations

- The command line options Username (`-U`), Password(`-P`) and Domain(`-D`) of the Storebrowse utility are case-sensitive and must be in upper case only.
