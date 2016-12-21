

This is a sample deployment/configuration repository which allows you to deploy a sample API Portal within minutes to any `docker` host.

## How to use This

Please refer to the official "Getting Started" documentation of the wicked.haufe.io microsite: [Getting Started](http://wicked.haufe.io/gettingstarted.html).

After your API Portal is up and running, you may continue trying out the API Portal according to e.g. the following document: [Using the Sample Portal](https://github.com/Haufe-Lexware/wicked.haufe.io/blob/master/doc/using-the-sample-portal.md).

## I don't want to read the Getting Started

Okay. This assumes you have `docker` 1.12 and `docker-compose` 1.8.0 or later running on your Windows, Linux or Mac OS X machine.

```
$ git clone https://github.com/Haufe-Lexware/wicked.deploy.sample
...
$ cd wicked.deploy.sample
$
```

Edit `/etc/hosts` (or similar) to make `portal.local` and `api.portal.local` point to `127.0.0.1`.

```
$ source ./env.sh
$ docker-compose up
...
```

This will take a while (1-5 minutes), depending on your bandwidth (docker needs to pull all images first). After it has settled down, you will see the first `ping` requests being served from `portal_1`:

```
portal_1                   | {"date":"09/Aug/2016:10:58:17 +0000","method":"GET","url":"/ping","remote-addr":"::ffff:172.20.0.2","user-id":"-","user-email":"-","version":"1.1","status":"200","content-length":"109","referrer":"-","user-agent":"-","response-time":"6.965","correlation-id":"c4de163e-e1bb-43c2-bc87-7f96598532d0"}
...
```

Now you can access the API Portal at [`https://portal.local`](https://portal.local). The browser will tell you the certificate is bad, but continue anyway.

## THIS IS A SAMPLE!

**Please read this** on why having a repository made like this one is really bad for production:

* This configuration repository has the SSL certificates checked in to git. And it's even a public repository, so that's very much a no go. These certificates are self signed and are only used (should only be used) for local deployments, so for a tutorial, it's okayish.
* Additionally, this repository has the "deployment key" (`PORTAL_CONFIG_KEY`) checked in to the `static` directory, as `deploy.envkey`. This is a super no-go in any case, as this key opens up the deployment API of the API Portal, and enables an attacker to read out any secrets stored in the configuration JSON files. So don't ever do that! We do it here to make sure everything works as desired.
* Likewise, you would never ever check in a file like `env.sh`, which is just a helper to set a bunch of environment variables. You would use some safe storage for that, like inside your build system, or vault or similar.
