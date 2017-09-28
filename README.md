# PHP source to image Helloworld Example

This is an example php application, which can be deployed to APPUiO using the following commands

## How to deploy

### Webconsole

* log into your OpenShift V3 Master Node
* Create a new Project
* "Add to Project" a php:5.6 application
* name the application for example appuio-php-sti-example and provide the git repository URL, in this example https://github.com/ejlp12/example-php-sti-helloworld.git
* the build and deployment is automatically triggered and the example application will be deployed soon

### CLI / oc Client

#### Create New OpenShift Project
```
$ oc new-project example-php-sti-helloworld
```

#### Create Application and expose Service
```
$ oc new-app https://github.com/ejlp12/example-php-sti-helloworld.git --name=indo-php-sti-example

$ oc expose service indo-php-sti-example
```

## Add Webhook to trigger rebuilds

Take the Webhook GitHub URL from

```
$ oc describe bc indo-php-sti-example

Name:		indo-php-sti-example
Namespace:	example-php-sti-helloworld
Created:	6 hours ago
Labels:		app=indo-php-sti-example
Annotations:	openshift.io/generated-by=OpenShiftNewApp
Latest Version:	4

Strategy:	Source
URL:		https://github.com/ejlp12/example-php-sti-helloworld.git
From Image:	ImageStreamTag openshift/php:7.0
Output to:	ImageStreamTag indo-php-sti-example:latest

Build Run Policy:	Serial
Triggered by:		Config, ImageChange
Webhook Generic:
	URL:		https://<HOSTNAME>:8443/oapi/v1/namespaces/example-php-sti-helloworld/buildconfigs/indo-php-sti-example/webhooks/9-kMuphDdqtNM7RSwUig/generic
	AllowEnv:	false
Webhook GitHub:
	URL:	https://<HOSTNAME>:8443/oapi/v1/namespaces/example-php-sti-helloworld/buildconfigs/indo-php-sti-example/webhooks/AAdE3mv-EzVLg9ajJAGd/github

```

and add the URL as a Webhook in your github Repository, read https://developer.github.com/webhooks/ for more details about github Webhooks
