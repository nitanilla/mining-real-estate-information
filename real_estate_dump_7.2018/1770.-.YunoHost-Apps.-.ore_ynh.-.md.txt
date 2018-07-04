# Open Real Estate app for YunoHost
[![Install ORE with YunoHost](https://install-app.yunohost.org/install-with-yunohost.png)](https://install-app.yunohost.org/?app=ore)
<br>
<b>website:</b>https://open-real-estate.info/ <br>
<b>Version:</b> 1.20.1 <br>
<b>Demo:</b> http://re-pro.monoray.net/en <br><br>
<b> *******Currently ORE can only be installed on root path. Eg. ore.domain.tld or domain.tld******* </b>

## Postinstallation
<b>You will have to do postinstallation manually.</b>

Add `/index.php?r=install/main/index` in front of your domain and and enter the database setting received through email.<br>
After this you need to set 'read-only' 644 right for the file <b>protected/config/db.php</b> with this command:
```bash
chmod 644 /var/www/opr/protected/config/db.php
```
## To-Do's
- [ ] Make upgrade script better so that sources get updated.
- [ ] Installtion on sub paths.
- [ ] Use curl for installation.
- [ ] Redirection to /index.php?r=install/main/index for postinstallation(if curl is used for the installation then this will not be needed)
