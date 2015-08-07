# Openshift Nginx Cartridge
[![OpenShift deploy](https://img.shields.io/badge/openshift-deploy-red.svg?style=flat-square)](https://openshift.redhat.com/app/console/application_type/custom?cartridges%5B%5D=https%3A%2F%2Fraw.githubusercontent.com%2FSamuelMoraesF%2Fopenshift-nginx%2Fmaster%2Fopenshift-cartridge-nginx)

This cartridge allow you to create a scalable nginx application.

Create your app using the deploy button above or with:

```BASH
rhc create-app nginx --env OPENSHIFT_NGINX_VERSION=1.7.10 https://raw.githubusercontent.com/SamuelMoraesF/openshift-nginx/master/openshift-cartridge-nginx
```

If you want to install a specific nginx version you can add `--env OPENSHIFT_NGINX_VERSION=<version>` to the command.
For example to install nginx 1.7.10 you can use:
```BASH
rhc create-app nginx --env OPENSHIFT_NGINX_VERSION=1.7.10 https://raw.githubusercontent.com/SamuelMoraesF/openshift-nginx/master/openshift-cartridge-nginx
```

## Versions
Currently this cartridge has the following versions:
- 1.6.2
- 1.7.10

If you need another version you can compile it yourself and submit a PR to get it integrated.

### Compiling a new version
To compile a new version you will first need a openshift application.
```BASH
rhc create-app nginx https://raw.githubusercontent.com/SamuelMoraesF/openshift-nginx/master/openshift-cartridge-nginx
```

Now clone the repository, create a `nginx` folder and copy the `usr/compile` directory from [this](https://github.com/boekkooi/openshift-cartridge-nginx) repository.
Set the versions you need to compile in the `nginx/compile/versions` file. Commit and push the application repository.
  
SSH into you app and go to the compile folder (`cd ${OPENSHIFT_REPO_DIR}/nginx/compile`) and start compiling by running the following command:
```BASH
./all
```
Once compiling is done you can download the `nginx.tar.gz` from you application. 
Extract the `nginx-{version}` from the archive and place them into the `openshift-nginx/usr` folder.
Last but not least edit the `openshift-nginx/manifest.yml` and add the versions.

All done just commit and push to your own `openshift-nginx` repo and use:
```BASH
rhc create-app nginx https://raw.githubusercontent.com/<you-username>/openshift-nginx/master/openshift-cartridge-nginx
```
