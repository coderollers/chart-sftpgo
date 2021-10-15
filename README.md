# Preamble
This is a Helm chart used to facilitate a deployment of [drakkan/sftpgo](https://github.com/drakkan/sftpgo).

It is a *very* early-stage piece of work and mostly used for quick and dirty testing. It might eventually evolve to a proper v1.0.0 implementation in order to support most if not all of the functionality which drakkan/sftpgo offers, but for now, feel free to fork it as the first stepping stone towards that.

Version 0.1.x as it is now only supports the default sqlite DB with persistent storage via Persistent Volume Claims, so nothing fancy.

# Installing or updating
You will require Helm v3. Build the chart first (it's not published anywhere yet).

> helm package .

The install or upgrade it within an existing namespace.

> helm -n sftpgo upgrade --install sftpgo ./sftpgo-0.1.0.tgz

Make sure you change the namespace, release and version accordingly.

Data will persist throughout upgrades. To see the SSH endpoint IP do

> kubectl -n sftpgo get svc

# Configuration
See the values.yaml file. You can override any of these values with your own values file and pass it on to helm.

After installation, you will need to configure it.

The Web app is not exposed for security reasons. To access it, you will need to first port-forward into it then open it in your browser at http://localhost:8080

> kubectl -n sftpgo port-forward $(kubectl -n sftpgo get pod|grep sftpgo|grep Running|awk '{print $1;}') 8080:8080

Note that user directories must be under `/srv/sftpgo`

Another note that the default URL will take you to the *client* login. For Admin login, go to http://localhost:8080/web/admin/login

# Removal
To remove it and all its data:

> helm -n sftpgo uninstall sftpgo

**WARNING**: This will remove all configuration and data!

# Contributing
Do you want to contribute to this? Wonderful! Make your changes and open a PR. Make sure you bump the version in the `Chart.yaml` file.

Have fun!
