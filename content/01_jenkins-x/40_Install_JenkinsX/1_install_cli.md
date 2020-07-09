+++

title = "Install CLI"
chapter = false
weight = 1

+++


Our first step is to install the CLI in order to use Jenkins X.  The CLI allows you to interact with the platform in different ways, including viewing pipelines, logs, creating PRs and much more.

There are binaries for various platforms including Linux and OS X.  In this scenario, I am using OS X, however, the installation is typical of any binary for your respective platform.

{{% notice info %}}
**NOTE:** As of the writing of this article, CJXD 8 is the latest binary version.
{{% /notice %}}

### Step 1 - Download binary
Download the jx binary archive by downloading the latest version using your web browser or by command-line using curl and pipe (|) the compressed archive to the tar command:

```bash
curl -L https://storage.googleapis.com/artifacts.jenkinsxio.appspot.com/binaries/cjxd/latest/jx-darwin-amd64.tar.gz | tar xzv
```

### Step 2 - Move binary to bin
Install the jx binary by moving it to a location in your executable path using the mv command:

```bash
sudo mv jx /usr/local/bin
```

### Step 3 - Test binary
Ensure you are using the correct binary and executable path with the which command:

```bash

#Check the binary version

➜ jx version
NAME               VERSION
jx                 2.0.1245+cjxd.8
Kubernetes cluster v1.14.10-gke.27
kubectl            v1.16.0
helm client        2.14.3
git                2.21.0
Operating System   Mac OS X 10.14.6 build 18G3020
 ```
 
When we downloaded the archive in step 1 above, a file called jx-requirements-eks.yml was also unarchived and placed in the directory where we executed the download command.  We will use that file in the next section.