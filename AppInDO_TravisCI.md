# Application in Digital Ocean
_Setup:_

## Setting up a Tomcat Server

Clone this repository [vagrant-for-tomcat](https://github.com/kploesser/vagrant-for-tomcat).

Replace the Vagrant file with [this](https://github.com/DatabaseGroup9/Documentation/blob/master/ApplicationServer/Vagrantfile)`.

Make sure to update the Vagrant file with the correct DigitalOcean tokenname, token and your ssh keys.

```vagrant up --provider=digital_ocean```

When the vagant script is completed a new Web Server with Tomcat has been installed.

## Travis CI deployment to Github
All commits to branch 'master' are automatically built and tested by Travis. If you want to mark a commit as ready for release, call:  
"git tag nameoftag"
where nameoftag contains 'rel' and today's date. Then, to push the tag,  
'git push origin master --tags' 
In order to include the tag in your push. No release will be deployed until a push is made with the --tags option.

### Getting the newest release
This command will wget info about the latest release, use jq to extract a download url for the .war file, then wget that:  
```"wget $(wget -qO- https://api.github.com/repos/DatabaseGroup9/ProjectGutenberg_G9/releases/latest | jq -r '.assets[] | select(.name | endswith(".war")) .browser_download_url')"```

### Automatically replace running webapp with newest
"/opt/tomcat/temp/getNewest.sh" downloads the newest release and replaces the current 'group9' app.
