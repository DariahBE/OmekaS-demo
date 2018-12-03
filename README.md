# OmekaS-demo
A proof of concept for crowdsourcing using Omeka S


## Goal
With the help of Omeka S design a platform to allow collaborators to transcribe Neobabylonian clay tablets. For this crowdsourcinig project, the focus was on transcribing based on images and connect it to other existing datasets. The original Nabucco dataset held references to locations, these are mapped to a dump of the Trismegistos places database which is included in the datafile. 

By using MediaWiki and the Omeka S Scripto module the requirement to crowd-source was fulfilled. This means that those wishing to collaborate need an account on MediaWiki and - when required - an account on the Omeka S instance.

## Notes
- The proof of concept is working, and usus images that are freely found on the web. In no means do they provide reliable transcriptions/interpretations.
- At this stage some of the Omeka S modules that are a part of this release do still contain bugs. Whenever possible we reported the bugs to the maintainer of the module.
- Omeka S installation requirements still apply see: https://omeka.org/s/docs/user-manual/install/#system-requirements 

## Deployment
This short guide assumes that you have a fully functioning LAMP stack to your availability. With a few simple steps you should be able to deploy this POC-release. 
1) Download the latest reslease: https://github.com/DariahBE/OmekaS-demo/releases 
2) Import both the SQL-files in your MYSQL instance.
3) Download and unzip omeka.zip to your www folder.
4) Download and unzip mediawiki.zip to your www folder.

### log in:
**WARNING**: We strongly suggest to change the usernames and passwords before deploying this release.
Access your mediawiki pages through your browser; you should find your mediawiki endpoint at http://www.localhost/<foldername> 
- The login credentials are:
  USERNAME: demo
  PASSWORD: Imtheadmin
  
Access your Omeka S instance through the browser; you should find your Omeka S endpoint at http://www.localhost/<foldername>
- The login credentails are:
   E-MAIL: me@exaple.com 
   PASSWORD: 3xample

### WARNINGS:

1) In case you use custom foldernames for your MediaWiki instance, then the API-endpoint that's needed to connect Omeka S with MediaWiki needs to be updated. (In fact, it's a good habit to check this before deploying).
The mediawiki endpoint is hosted in the root folder of your MediaWiki instance and is called 'api.php'. e.g. if your loginpage is at: http://www.localhost/mediawiki then the endpoint is at http://www.localhost/mediawiki/api.php
 -  Log in to your Omeka S instance as admin.
 -  On the left hand side click 'Modules'
 -  Look for the module called 'scripto' and click 'configure'
 -  You can now update the location for the MediaWiki endpoint.
 -  Click submit to store the changes.

2) The Omeka S instance is still in debugging mode, whenever an error occurs you (and your visitors) will see a nasty stacktrace. These come in handy when investigating/reporting bugs; but are a nuissance for visitors. You can go out of debugging mode by removing 
´´´SetEnv APPLICATION_ENV "development"´´´ in the .htaccess file. The easiest way of achieving this is to open the folder in the terminal and type: ´´´´sudo nano .htaccess´´´

3) The Omeka S relative paths rely on rewriterules. For this it's crucial to enable mod_rewrite and set the AllowOverrid to 'All'. For more info: https://omeka.org/s/docs/user-manual/install
