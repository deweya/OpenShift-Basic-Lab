# Prerequisite: Minishift - Your personal OpenShift cluster
A production-ready OpenShift cluster can take upwards of an hour to install, and that's assuming everything goes right the first time! Minishift, on the other hand, is a tool that will quickly spin up a single-node OpenShift cluster, removed of some of the more complex bells and whistles. To a developer there is virtually no difference between the two.

For the prerequisite, we'll install minishift on your local machine so that in the `lab/`, we can spend the time diving into some of the cool features of OpenShift!

## Install Minishift
Visit this link https://developers.redhat.com/products/cdk/download and download version 3.7.0 for your OS. You'll have to authenticate with either you employee rhn-gps-* credentials, or click "Create one now" at the bottom of the screen to create a Red Hat Developers account.

The downloaded file may be given a name like "cdk-3.7.0-*". If so, rename this file to "minishift":
```
mv cdk-3.7.0-* minishift
```

The file as-is does not have "execute" permission. Be sure to apply the proper permission on the file:
```
chmod u+x minishift
```

For convenience, you should also move this file to somewhere managed by your PATH variable, for example, "/usr/local/bin":
```
sudo mv minishift /usr/local/bin
```

## Install VirtualBox
Minishift relies on a hypervisor to install the cluster inside a VM. Download the latest version of VirtualBox (https://www.virtualbox.org/). You can also install VirtualBox with your package manager, for example:
```
sudo yum install -y VirtualBox
```

## Configure Minishift
In order to run Minishift, we need to set up some required components. Luckily, Minishift makes this easy - run this command:
```
minishift setup-cdk
```

This command installs several components to your `~/.minishift` directory. One of these components is the `oc` command, which is the cli tool used to communicate with an OpenShift cluster. Copy this command somewhere managed by your PATH variable:
```
sudo cp -a ~/.minishift/cache/oc/v3.11.43/linux/oc /usr/local/bin
```

We're almost done! The last thing to do is to tell Minishift to use VirtualBox as its hypervisor:
```
minishift config set vm-driver virtualbox
```

## Run Minishift
At this point you should technically be finished, but to be safe, let's make sure that minishift is working properly.

Start a new OpenShift cluster:
```
minishift start
```

After a minute or two, you will be asked to provide your rhn-gps-* or Red Hat Developers credentials in order to register the VM with subscription-manager.

If everything has been configured properly, the command will take around 5-10 minutes to complete. You will know that the command has exited properly when you see the credentials and URL to the OpenShift master.

Minishift provides a convenient command that you can run once installation is complete:
```
minishift console
```

This will take you to the OpenShift UI. Note that you will probably have to confirm a security exception on your browser, since OpenShift is configured to use self-signed certificates by default.

Congrats on spinning up your first OpenShift cluster in Minishift! Now that you have a cluster up and running, you may now complete the `../lab/`!
