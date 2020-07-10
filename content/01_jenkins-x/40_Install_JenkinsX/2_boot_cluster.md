+++

title = "Install Jenkins X on EKS Cluster Using Jenkins X Boot"
chapter = false
weight = 2

+++


Assuming you have an EKS cluster provisioned, and you are able to connect to it from your desktop with proper credentials, we can now focus on installing Jenkins X on top of said cluster.  

{{% notice info %}}
**NOTE:** As of the writing of this article, CJXD 8 is the latest binary version.
{{% /notice %}}

### Step 1 - Modify the jx-requirements-eks.yml file with basic settings
The basic settings we will modify in order to execute an initial jx boot installation will be as follows (please modify your file accordingly)

```yaml
cluster:
 clusterName: drymartini  # cluster name from when you created the eks cluster
 environmentGitOwner: jenkins-oscar #GitHub Org
 environmentGitPublic: true #Repos are public
 provider: eks
 region: us-west-2
```

The environmentGitOwner is the GitHub Organization name.  Because I am using the free tier of GitHub, my repositories must be publicly accessible.  Therefore, the environmentGitPublic field is set to true.  The rest of the fields are self-explanatory.

The domain is specified within the ingress field and child elements as shown.

```yaml
ingress:
 domain: jx.eks.sharepointoscar.com
 externalDNS: true
 ignoreLoadBalancer: true
 namespaceSubDomain: -jx.
 tls:
   email: me@sharepointoscar.com
   enabled: true
   production: true
```

#### HashiCorp Vault Initial Configuration

In order for the jx boot command to run successfully the first time, we need to specify an IAM username in the specific jx-requirements-eks.yml file section as follows:

```yaml 
vault:
 aws:
   autoCreate: true
   iamUserName: aws_admin@sharepointoscar.com
 disableURLDiscovery: true
```

{{% notice info %}}
**TIP:** For details on IAM permissions, please refer to the [documentation](https://docs.cloudbees.com/docs/cloudbees-jenkins-x-distribution/latest/eks-install-guide/aws-iam-permissions).
{{% /notice %}}



### Step 2 - Execute JX Boot CLI Command
Having modified the appropriate fields in the jx-requirements-eks.yml, we are ready to execute the jx boot CLI command as follows:

```bash
jx boot -r jx-requirements.eks.yml
```

{{% notice warning %}}
**TIP:** Note that this command is executed in the same location where the requirements file is located.
  However, any future executions of jx boot, will require you to execute it from the root of the cluster configuration repository that was cloned during the first run.  This effectively means the original jx-requirements-eks.yml file is no longer used in subsequent executions.
{{% /notice %}}



You will answer a few questions, which include:

1.  A comma-separated list of **GitHub usernames** that can be approvers for PRs issued against the configuration repository, otherwise known as the Dev Repository.


2. You will get a warning stating HashiCorp Vault is enabled and TLS is not.  Answer **Y** to that question, as we are in fact setting up TLS and a custom domain.

3. Hit enter to accept the creation of long term storage S3 buckets.

4. Type the Jenkins X Admin account username, and password

5. Specify the **pipelineusername**, this is your GitHub bot account name.  In addition you will be asked for an email adddress and a token for this account.

6. Configure External Docker?  Answer **N** as we use ECR by default.

Jenkins X goes through a verification of configuration on the newly created environment, you should see the last output from the install look something similar to the following:

```bash
POD                                            STATUS
crier-6c4944b868-wccgk                         Running
deck-7f5c64b45d-cdhpv                          Running
deck-7f5c64b45d-xsqgs                          Running
exdns-external-dns-545998d78d-spcvf            Running
hook-647f968ffb-95n99                          Running
hook-647f968ffb-b4ppb                          Running
horologium-9fdcd6b57-cbgwq                     Running
jenkins-x-chartmuseum-d87cbb789-qj878          Running
jenkins-x-controllerbuild-5b87d6f59c-4nb6v     Running
jenkins-x-controllerrole-55fbf89ccc-t2b5b      Running
jenkins-x-heapster-75558b6cfb-8vszj            Running
jenkins-x-nexus-8b8dfd746-cjzrk                Running
jx-vault-drymartini-0                          Running
jx-vault-drymartini-configurer-769ffcd54-5hq8x Running
pipeline-7dff794486-qkmvt                      Running
pipelinerunner-7c747569d4-d8n9l                Running
tekton-pipelines-controller-666488cbd5-gbw29   Running
tide-6bcf8f9f7f-klz2n                          Running
vault-operator-75d5446bb7-8f6w9                Running
Verifying the git config
Verifying username jenkinsx-bot-sposcar at git server github at https://github.com
Found 1 organisations in git server https://github.com: jenkins-oscar
Validated pipeline user jenkinsx-bot-sposcar on git server https://github.com
Git tokens seem to be setup correctly
Installation is currently looking: GOOD
```

Now that we have our installation working, we should also be able to see the endpoints created by executing jx get urls

```bash
>$ jx get urls

NAME                URL
deck                https://deck-jx.jx.eks.sharepointoscar.com
hook                https://hook-jx.jx.eks.sharepointoscar.com
jx-vault-drymartini https://vault-jx.jx.eks.sharepointoscar.com
nexus               https://nexus-jx.jx.eks.sharepointoscar.com
tide                https://tide-jx.jx.eks.sharepointoscar.com
```