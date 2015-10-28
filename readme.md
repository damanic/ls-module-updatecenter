#Update Center Module
###Lemonstand Version 1
#####Update modules from GitHub using the backend `Modules & Updates' tool! 
This module also allows you to continue to receive lemonstand marketplace updates even if you have updated your core modules beyond Lemonstand's last version release.

#Install
Install this module through the marketplace as normal. Once installed:

- Download the latest release zip/tar archive: https://github.com/damanic/ls1-module-updatecenter/releases
- Unzip so the folder `updatecenter` is added to your /modules directory
- Go to {youradminurl}/updatecenter/setup/
- Click the 'Status' tab
- Patch the core (warning: read core patch info below)

#Core Patch
The lemonstand module located at /modules/core is no longer receiving updates from Lemonstand. In order to use this module the core module requires a patch. This patch replaces three files:

- /modules/core/helpers/core_ziphelper.php
- /modules/core/classes/core_updatemanager.php
- /modules/core/thirdpart/pclzip.lib.php

It adds new trigger events to Core_UpdateManager, a new function to the zip helper and upgrades to the latest PclZip library.

If you have made your own edits to these files since the final lemonstand release you can manually install/compare the files included in /modules/updatecenter/updates/core/

#GitHub Repository Updates
Update one or more versioned modules in the /modules/ directory from public GitHub releases.

#Other Repository Support
Drivers for other public repositories can be added on request. Contributions welcome via:  https://github.com/damanic/ls1-module-updatecenter

#Repository Config
The update center can be pointed to a public repository for each module on the system by a config file. Config files are  located in /modules/updatecenter/repositories/

Out of the box a fully functional repo config file is available for selection via {youradminurl}/updatecenter/setup/.  Selecting this config file will update lemonstand from https://github.com/damanic/ with the latest release for this module along with maintanence updates to core modules.  You can view the config at /modules/updatecenter/repositories/damanic/info.php.  Do not edit this file as it may be overwritten on future updates to this module.  You can however copy it to a new config file and extend/edit it as you like.
 
#Adding Custom Repository Config Files
Copy the contents of /modules/updatecenter/repositories/damanic/info.php to /modules/updatecenter/repositories/{yourfolder}/info.php.  Edit the name, description and repositories data.  Once saved it will be available for selection from {youradminurl}/updatecenter/setup/. Each config file you add must reside in its own folder.

#Example Config File
```

	$repository_info = array(
		'name'=>'Core Module Updates (daManic)',
		'description'=>'Bugfixes and new event additions to core modules no longer updated by lemonstand (cms,core,etc). Plus updates to the updatecenter module.',

		'repositories' => array(
			array(
				'source' =>	'github',
				'modules' => array(
					'core' => array(
						'owner' => 'damanic',
						'repo' => 'ls1-module-core'
					),
					'cms' => array(
						'owner' => 'damanic',
						'repo' => 'ls1-module-cms'
					),
					'updatecenter' => array(
						'owner' => 'damanic',
						'repo' => 'ls1-module-updatecenter'
					)
				)
			)

		),

	);
	
```

#Your GitHub Repo
If you are adding your own repo as a source to update a module there are a few things you need to do:

- Make sure your module directory structure is compatible with lemonstands module requirements. The /updates/version.dat MUST be present in the repository in order for the update to succeed.
- Lemonstand will only update from the latest  'release' issued by your repository. See: https://help.github.com/articles/creating-releases/
 
#Limitations
The repo updates will only update modules in the /module/ directory. It does not support updates to the framework outside of this directory.
 
#Update Blocking
- Set from 'block' tab in :  {youradminurl}/updatecenter/setup/
- Select any module that you would like the update center to block from receiving updates. This applies to both repo and the lemonstand update delivery service.

#Forced Updates
Using the forced update button when no updates are found forces lemonstand to re-download the modules and overwite them: 
- First all the final/latest releases from the lemonstand update service are extracted to the modules directory.
- Second all the latest releases from your repositories are extracted to the modules directory.

#Common Issues
###Update process successfully completed but update did not apply
If a module has been added to your modules directory via FTP or not via lemonstands update manager, the files may not be PHP writable.
Any file in a module directory that is not PHP writable will not be updated. Be sure to CHMOD the files and folders in your /modules directory so that it is PHP writable after any manual file upload.
