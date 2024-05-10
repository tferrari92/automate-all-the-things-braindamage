<a href="https://www.instagram.com/ttomasferrari/">
    <img align="right" alt="Abhishek's Instagram" width="22px" 
    src="https://i.imgur.com/EzpyGdV.png" />
</a>
<a href="https://twitter.com/tomasferrari">
    <img align="right" alt="Abhishek Naidu | Twitter" width="22px"         
    src="https://i.imgur.com/eFVBTVz.png" />
</a>
<a href="https://www.linkedin.com/in/tomas-ferrari-devops/">
    <img align="right" alt="Abhishek's LinkedIN" width="22px" 
    src="https://i.imgur.com/pMzVPqj.png" />
</a>
<p align="right">
    <a >Find me here: </a>
</p>
<!-- <p align="right">
    <a  href="/docs/readme_es.md">Versión en Español</a>
</p> -->

<p title="All The Things" align="center"> <img src="https://i.imgur.com/9wX6ADr.jpg"></p>


# **BRAINDAMAGE EDITION**

This Braindamage Edition builds upon the [Overload Edition](https://github.com/tferrari92/automate-all-the-things-overload).

### New features:

- Developer Portal with Backstage.io

### Versions in order of complexity:

1. [Regular Edition](https://github.com/tferrari92/automate-all-the-things)
2. [Hardcore Edition](https://github.com/tferrari92/automate-all-the-things-hardcore)
3. [Insane Edition](https://github.com/tferrari92/automate-all-the-things-insane)
4. [Overload Edition](https://github.com/tferrari92/automate-all-the-things-overload)
5. [Braindamage Edition](https://github.com/tferrari92/automate-all-the-things-braindamage)
7. [Nirvana Edition](https://github.com/tferrari92/automate-all-the-things-nirvana)
<!-- 6. [Transcendence Edition](https://github.com/tferrari92/automate-all-the-things-transcendence)  -->

### Spin-offs:
- [Backstage Minikube Lab](https://github.com/tferrari92/backstage-minikube-lab)

<br/>

# **INDEX**

- [Introduction](#introduction)
  - [Prerequisites](#prerequisites)
  - [What we'll be doing](#what-well-be-doing)
  - [Tools we'll be using](#tools-well-be-using)
  - [Disclaimer](#disclaimer)
- [Local Setup](#local-setup)
- [GitHub Actions Setup](#github-actions-setup)
  - [Get your AWS keys](#get-your-aws-keys)
  - [Create secrets for GitHub Actions](#create-secrets-for-github-actions)
- [Backstage.io](#backstageio)
  - [Prerequisites](#prerequisites)
  - [Initial setup](#create-secrets-for-github-actions)
   - [Get GitHub PAT](#get-github-pat-personal-access-token)
  - [Run Backstage locally](#run-backstage-locally)
  - [Customising Backstage](#customising-backstage)
    - [Plugins I've added](#plugins-ive-added)
    - [Templates I've created](#templates-ive-created)
    - [My arbitrary rules](#my-arbitrary-rules)
  - [Meme-Web](#meme-web)
- [AWS Infrastructure Deployment Pipeline](#aws-infrastructure-deployment-pipeline)
  - [Description](#description)
  - [Instructions](#instructions)
- [About ArgoCD Sync Waves](#about-argocd-sync-waves)
  - [ArgoCD Self-Manage Applications](#argocd-self-manage-applications)
  - [App of Apps](#app-of-apps)
  - [Backend Applications](#backend-applications)
  - [Frontend Applications](#frontend-applications)
- [ArgoCD Deployment Pipeline](#argocd-deployment-pipeline)
  - [Description](#description-1)
  - [Instructions](#instructions-1)
- [Sealed Secrets Pipeline](#sealed-secrets-pipeline)
  - [Description](#description-2)
  - [Instructions](#instructions-2)
<!-- - [Backend Service Build & Deploy Pipeline](#backend-service-build--deploy-pipeline)
  - [Description](#description-3)
  - [Instructions](#instructions-3)
- [Frontend Service Build & Deploy Pipeline](#frontend-service-build--deploy-pipeline)
  - [Description](#description-4)
  - [Instructions](#instructions-4) -->
- [Kubernetes Tools Management](#kubernetes-tools-management)
  - [Description](#description-5)
  - [Instructions](#instructions-5)
- [Destroy All The Things Pipeline](#destroy-all-the-things-pipeline)
  - [Description](#description-6)
  - [Instructions](#instructions-6)
- [Conclusion](#conclusion)
  - [On the next edition](#on-the-next-edition)

<br/>

# **INTRODUCTION**

I believe in a world where all that's expected of me is to enjoy life, lay on the couch, play COD and have existential crises.

I wish I could automate cooking, cleaning, working, doing taxes, making friends, dating and even writing stupid READMEs.

But technology hasn't quite caught up to my level of laziness yet, so I've taken some inspiration from Thanos and said ["Fine... I'll do it myself"](https://www.youtube.com/watch?v=EzWNBmjyv7Y).

Here's my attempt at making the world a better place. People in the future will look back at heroes like me and enjoy their time playing video games and fighting the war against AI, in peace.

<br/>

## Prerequisites

- [Git installed](https://www.python.org/downloads/)
- [Python3 installed](https://www.python.org/downloads/)
- [Active GitHub account](https://github.com/)
- [Active DockerHub account](https://hub.docker.com/)
- [Active AWS account](https://aws.amazon.com/)

<br/>

## What we'll be doing

<p title="Diagram" align="center"> <img img width="800" src="https://i.imgur.com/HeuvWw9.jpg"> </p>

<br/>

The purpose of this repo is not to give you an in depth explanation of the tools we'll be using, but to demonstrate how they can interact with each other to make the deployment of a whole infrastructure (with an application) as efficient and streamlined as possible.

I want to show how IaC (Infrastructure as Code), Gitops and CI/CD (Continuous Integration/Continuous Deployment) can be merged for [unlimited power](https://www.youtube.com/watch?v=Sg14jNbBb-8).

As you can see in the diagram, we'll be deploying an EKS Kubernetes cluster in AWS. Inside the cluster we'll have three environments where our app will be deployed. The app is made up of two microservices: frontend and backend. Each frontend will be accesible to the public internet through a Load Balancer.

Along with the cluster, we'll deploy an ElastiCache (Redis) database for each environment and one EC2 instance for running configuration tasks on the databases. We'll also create an S3 bucket which will store our terraform state file.

Our app is a very simple static website, but I'm not spoiling it for you. You'll have to deploy it to see it.

<br/>

## Tools we'll be using

- Code Versioning -> Git
- Source Code Management -> GitHub
- Cloud Infrastructure -> Amazon Web Services
- Infrastructure as Code -> Terraform
- Containerization -> Docker
- Container Orchestration -> Kubernetes
- Continuous Integration -> GitHub Actions
- Continuous Deployment -> Helm & ArgoCD
- Scripting -> Python
- Monitoring -> Prometheus
- Logging -> Loki
- Observavility Visualization -> Grafana
- Service Mesh -> Istio
- Canary Deployments -> Flagger
- Service Mesh Visualization -> Kiali
- Kubernetes Secrets Encryption -> Bitnami Sealed Secrets
- Code Instrumentation -> OpenTelemetry
- Tracing -> Jaeger
- Internal Developer Platform -> Backstage.io

<br/>

<p title="Logos Banner" align="center"> <img  src="https://i.imgur.com/mt4dNO3.png"> </p>

<br/>

## Disclaimer

This is not a free project, it will cost you between $1 US dollars and $10 depending on how long you run the resources for. That's assuming you run them for a few hours tops, not days. Always remember to run the [destroy-all-the-things pipeline](/.github/workflows/04-destroy-all-the-things.yaml) when you are done.

Some things could have been further automated but I prioritized modularization and separation of concerns.<br>

For example, the EKS cluster could have been deployed with ArgoCD installed in one pipeline, but I wanted to have them separated so that each module is focused on its specific task, making each of them more recyclable.

Also, please do submit an issue if you find any errors or you have any good ideas on how to improve this, I would love to hear them.

Let's begin...

<br/>
<br/>
<p title="Automation Everywhere" align="center"> <img width="460" src="https://i.imgur.com/xSmJv0k.png"> </p>
<br/>

---

<br/>

# **LOCAL SETUP**

In order to turn this whole deployment into your own thing, we need to do some initial setup:

1. Fork this repo. Keep the repository name "automate-all-the-things-braindamage".
1. Clone the repo from your fork:

```bash
git clone https://github.com/<your-github-username>/automate-all-the-things-braindamage.git
```

2. Move into the directory:

```bash
cd automate-all-the-things-braindamage
```

2. Run the initial setup script. Come back when you are done:

```bash
python3 python/initial-setup.py
```

4. Hope you enjoyed the welcome script! Now push your customized repo to GitHub:

```bash
git add .
git commit -m "customized repo"
git push
```

5. Awesome! You can now proceed with the GitHub Actions setup.

<br/>
<br/>
<p title="Evil Kermit" align="center"> <img width="650" src="https://i.imgur.com/pIGcI2d.jpg"> </p>
<br/>
<br/>


# **GITHUB ACTIONS SETUP**

Before running our pipelines we need to get a few things set up<br>

## Get your AWS keys

These will be required for our workflows to connect to your AWS account.

1. Open the IAM console at https://console.aws.amazon.com/iam/.
2. On the search bar look up "IAM".
3. On the IAM dashboard, select "Users" on the left side menu. _If you are root user and haven't created any users, you'll find the "Create access key" option on IAM > My security credentials. You should know that **creating Access Keys for the root user is a bad security practice**. If you choose to proceed anyway, click on "Create access key" and skip to point 6_.
4. Choose your IAM user name (not the check box).
5. Open the Security credentials tab, and then choose "Create access key".
6. To see the new access key, choose Show. Your credentials resemble the following:

- Access key ID: AKIAIOSFODNN7EXAMPLE<br>
- Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

7. Copy and save these somewhere safe.

<br/>

## Create secrets for GitHub Actions

1. Go to the Settings tab of your GitHub repo.
2. On the left-side menu click "Secrets and variables" and then on "Actions".
3. Under "Repository secrets" click on "New repository secret".
<p title="Guide" align="center"> <img width="700" src="https://i.imgur.com/656voMj.png"> </p>

4. Under "Name" write "AWS_ACCESS_KEY_ID" and under "Secret" paste the corresponding value. 
5. Click "Add secret" to save.
6. Repeat the process for:
- AWS_SECRET_ACCESS_KEY
- DOCKER_USERNAME
- DOCKER_PASSWORD

<br/>
<br/>
<p title="We Are Not The Same" align="center"> <img width="460" src="https://i.imgur.com/E0s8TW6.png"> </p>
<br/>
<br/>

---

<br/>
<br/>

# BACKSTAGE.IO

Before deploying our infra, let's explore Backstage locally.

Backstage is a framework for creating developer portals. This developer portal should act as a centralized hub for your organization, providing access to documentation, infrastructure, tooling, and code standards. It gives developers everything they need to create and manage their projects in a consistent and standardized manner. If you are new to Backstage, I invite you to read [this brilliant series of articles](https://www.kosli.com/blog/evaluating-backstage-1-why-backstage/) by Alexandre Couedelo.

If you want to test Backstage out before you start spending money on AWS, I suggest you try out my [Backstage Minikube Lab](https://github.com/tferrari92/backstage-minikube-lab).

</br>

## Prerequisites
- nodejs installed
- nvm installed
- yarn installed

</br>

## Initial setup
Before deploying Backstage in a EKS, we need to build it locally.

`cd` into my-backstage directory
```bash
cd backstage/my-backstage/
```

Make sure you are using Node.js version 18
```bash
nvm install 18
nvm use 18
nvm alias default 18
```


Make sure you are using Yarn version 1.22.19
```bash
yarn set version 1.22.19
yarn --version
```
</br>

### Get GitHub PAT (Personal Access Token)

Navigate to the GitHub PAT creation page. Select "Generate new token (classic)". 

Choose a name and a value for expiration. Under scopes select "repo" and "workflow". It should look something like this:

<p title="GitHub Token" align="center"> <<img width="650" src="https://i.imgur.com/zTn7gDI.png"> </p>

Click Generate token. Store the token somewhere safe.

</br>

## Run Backstage locally
Everything's ready to start playing with Backstage.

Create env var for your GitHub token
```bash
export GITHUB_TOKEN=<your-github-token>
```

Then run
```bash
yarn install
yarn tsc
yarn dev
```

Open your browser and go to localhost:3000. You should see the Backstage web UI.

Every time you make changes to the Backstage code, it's recommended you test it by running it locally with "yarn dev" like you just did. This will be much faster that testing every change in EKS.

</br>

## Customising Backstage
Before deploying our infra, lets go over some things you'll find in this Backstage deployment.

Backstage is designed to be flexible and allow every organization to adapt it to their own needs. It is not a black-box application where you install plugins; rather, you maintain your own source code and can modify it as needed.

I've already added some custom stuff to the default Backstage installation that I think are essential. 

</br>

### Plugins I've added

#### - Kubernetes plugin
The [Kubernetes plugin](https://backstage.io/docs/features/kubernetes/) in Backstage is a tool that's designed around the needs of service owners, not cluster admins. Now developers can easily check the health of their services no matter how or where those services are deployed — whether it's on a local host for testing or in production on dozens of clusters around the world.

It will elevate the visibility of errors where identified, and provide drill down about the deployments, pods, and other objects for a service.
</br>

#### - GitHub Discovery plugin 
The [GitHub Discovery plugin](https://backstage.io/docs/integrations/github/discovery) automatically discovers catalog entities within a GitHub organization. The provider will crawl the GitHub organization and register entities matching the configured path. This can be useful as an alternative to static locations or manually adding things to the catalog. This is the preferred method for ingesting entities into the catalog.

I've installed it without events support. Updates to the catalog will rely on periodic scanning rather than real-time updates.

You can check the automatic discovery configuration under catalog.providers.github in the [app-config.yaml](/backstage/my-backstage/app-config.yaml) and [app-config.production.yaml](/backstage/my-backstage/app-config.production.yaml) files.

**IMPORTANT**: We use [app-config.yaml](/backstage/my-backstage/app-config.yaml) for local testing (when running `yarn dev`) and [app-config.production.yaml](/backstage/my-backstage/app-config.production.yaml) when deploying to Minikube.

</br>

### Templates I've created

#### - New Backstage System
Creates a new Backstage System with the provided information. A System in Backstage is a collection of entities (services, resources, APIs, etc.) that cooperate to perform a some function. For example, we will have a System called "my-app" that includes the my-app-frontend service, the my-app-backend service, the my-app-redis database and the my-app-backend API.

It generates a Pull Request which includes a new System manifest. When merged, the System catalog entity will be automatically added to the Backstage catalog by the GitHub Discovery plugin.
</br>

#### - New Backstage Group
Creates a new Backstage group with the provided information. 

It generates a Pull Request which includes a new Group manifest. When merged, the Group catalog entity will be automatically added to the Backstage catalog by the GitHub Discovery plugin.
</br>

#### - New Backstage User
Creates a new Backstage user with the provided information. 

It generates a Pull Request which includes a new User manifest. When merged, the User catalog entity will be automatically added to the Backstage catalog by the GitHub Discovery plugin.
</br>

#### - New Node.js in existing repo
Creates all the boilerplate files and directories in an existing repo for deploying a new Node.js service in Kubernetes:
1. The application code directory and files, which will saved in [the application-code directory](/application-code/).
2. The helm chart, which will be saved in [the helm-charts/systems directory](/helm-charts/systems/).
3. The application.yaml files which will be saved in [the argo-cd/applications/systems/ directory](/argo-cd/applications/systems/).
4. The build and deploy GitHub workflow manifest, which will be saved [the .github/workflows directory](/.github/workflows/) (working with GitHub Workflows is out of the scope of this lab).

It generates a Pull Request which includes all these files al directories.
</br>

#### - New NGINX in existing repo
Creates all the boilerplate files and directories in an existing repo for deploying a new NGINX service in Kubernetes:
1. The application code directory and files, which will saved in [the application-code directory](/application-code/).
2. The helm chart, which will be saved in [the helm-charts/systems directory](/helm-charts/systems/).
3. The application.yaml files which will be saved in [the argo-cd/applications/systems/ directory](/argo-cd/applications/systems/).
4. The build and deploy GitHub workflow manifest, which will be saved [the .github/workflows directory](/.github/workflows/) (working with GitHub Workflows is out of the scope of this lab).

It generates a Pull Request which includes all these files al directories.

</br>

### My Arbitrary Rules

#### - App-config management 
The app-config is the file that defines the Backstage configuration. You will find three instances of app-config:
1. [The app-config.yaml file](/backstage/my-backstage/app-config.yaml): This is the config that will be used for development and testing purposes when running locally with `yarn dev` command.
2. [The app-config.production.yaml file](/backstage/my-backstage/app-config.production.yaml): This is the config that will be used for building the Docker image that will be deployed in Minikube. You will notice that it's missing the catalog configuration. That's because the catalog configuration will be passed in through a ConfigMap.
3. [The helm chart values-custom.yaml file](/helm-charts/infra/backstage/values-custom.yaml): Since the catalog configuration is something that might need to be modified more often, I decided it should be specified in a ConfigMap and not hard coded into the Docker image. You can find the catalog configuration in the values-custom.yaml file of the Backstage helm chart. Helm will create a ConfigMap with these values and pass it in to the Backstage pod at the time of creation.
</br>

#### - Users and groups hierarchy
I decided that user and group hierarchy should be defined from the bottom up. To me, it makes more sense that childs should keep track of their parents than parents of their childs.

So we will not define the members of a group in the Group manifest, but we will define the group a user belongs to in the spec.memberOf of the User manifest. 

Also, we will always have the spec.children value of Group manifests as an empty array and the spec.parent value filled with whoever the parent group of that group is. If it has no parent, the value of spec.parent should be "root".

</br>

## Meme-Web

I've left the meme-web as an example so that you can use it as reference when deploying your new systems, users, groups, services, etc. These are some of the files you might want to check out:
- [component](/application-code/meme-web/backend/catalog-info.yaml)
- [resource](/application-code/meme-web/redis/catalog-info.yaml)
- [api](/application-code/meme-web/backend/api-info.yaml)
- [system](/backstage/entities/systems/meme-web.yaml)
- [group](/backstage/entities/groups/meme-web-team.yaml)
- [user](/backstage/entities/users/geralt.yaml)


<br/>
<br/>
<p title="Hard right" align="center"> <img width="460" src="https://i.imgur.com/Stl0y81.jpg"> </p>
<br/>
<br/>


# AWS INFRASTRUCTURE DEPLOYMENT PIPELINE

## Description

Our first pipeline, the one that will provide us with all the necessary infrastructure.

What does this pipeline do? If you take a look at the [01-deploy-infra.yml](/.github/workflows/01-deploy-infra.yaml) file, you'll see that the first thing we do is use the Terraform plugin we previously installed to deploy a S3 Bucket and DynamoDB table. These two resources will allow us to store our terraform state remotely and give it locking functionality.<br/>

Why do we need to store our tf state remotely and locking it? Well, this is probably not necessary for this exercise but it's a best practice when working on a team.<br>
Storing it remotely means that everyone on the team can access and work with the same state file, and locking it means that only one person can access it at a time, this prevents state conflicts.

Before we proceed with deploying our actual infrastructure, the pipeline will move the state file to the [terraform/aws/ directory](/terraform/aws/), so our backend resources (the Bucket and DynamoDB Table) will also be tracked as part of our whole infrastructure. If you want to understand how this works, I suggest you watch [this video](https://youtu.be/7xngnjfIlK4?t=2483) where Sid from [DevOps Directive](https://www.youtube.com/@DevOpsDirective) explains it better than I ever could.

Now that the backend is set, we will deploy our actual infrastructure!

So, what is our infra? Well, the main parts are the networking resources, the ElastiCache databases, the EC2 instance and the EKS cluster, along with the Cluster Autoscaler, EBS CSI driver and an AWS Load Balancer Controller which will act as our Kubernetes Ingress Controller.

Having this AWS Load Balancer Controller means that for every Ingress resource we create in our cluster, an AWS Application Load Balancer will be automatically created. This is the native way to do it in EKS and it has a lot to benefits, but it creates an issue for us.<br>
We want to track everything in our infra as IaC, but these automatically created Application Load Balancers won't be tracked in our Terraform... No worries, we'll take care of this issue in the Destroy All The Things Pipeline.<br>
For more info on the AWS Load Balancer Controller you can watch [this excellent video](https://youtu.be/ZfjpWOC5eoE) by [Anton Putra](https://www.youtube.com/@AntonPutra).

In this Insane Edition, apart from the AWS Load Balancer, we'll also be using an Istio Ingress Gateway. Our app (on the three environments) will be accesed through the Istio Ingress Gateway. All other services (ArgoCD, Grafana, etc.) will still be accessed in the previous manner through Ingresses and the AWS Load Balancer. 

If you want to know exactly what is being deployed, you can check out the [terraform files](/terraform/aws). Here you can modify the resources to be deployed to AWS. Let's say you want to add a second EC2 Instance, you can add the following block in the ec2.tf file:

```terraform
resource "aws_instance" "ec2_instance" {
    ami = "ami-01107263728f3bef4"
    subnet_id = aws_subnet.public-subnet-a.id
    instance_type = "t2.micro"
}
```

Commit the changes and run the pipeline again. The backend deployment step will fail, so the pipeline will finish with a warning, you can ignore it.

The pipeline will also modify the [helm-charts/systems/my-app/backend/environments](/helm-charts/systems/my-app/backend/environments) files on the repo. It will get the endpoints for each ElastiCache DB from terraform outputs and include them in the values of each environment.

Oh and lastly... it will export an artifact with the instructions on how to connect to the EC2 instance.

<br/>

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "01-Deploy AWS infrastructure" workflow.
3. Click on "Run workflow" (Use workflow from Branch: main).
4. When it's finished, the EC2 instance public IP address will be exported as an artifact. You'll find it in the workflow run screen under "Artifacts". Download it to see the instructions to access the instance.

<br/>
<br/>
<p title="Kevin James" align="center"> <img width="460" src="https://i.imgur.com/ULcCyVx.jpg"> </p>
<br/>
<br/>

# ABOUT ARGOCD SYNC WAVES

We have A LOT going on right now, it's getting out of control. Let's get our shit together, together.

We will implement ArgoCD Sync Waves. Through a simple annotation in our manifests, we can tell ArgoCD in which order our resources should be deployed. We basically give each manifest a number (which can be negative too) which defines what its place in the deployment sequence is.

This means we shouldn't worry anymore about in which order our pipelines are run, ArgoCD will always make sure that, for example, the backend is successfully deployed before applying the frontend manifests.

You will see that not all manifests have the ArgoCD Sync Wave annotation. If I didn't give a manifest a Sync Wave number it's because it doesn't generate any conflicts in terms of the order in which it's deployed. By default they will get a "0" sync wave priority.

The sequence will go like this: 
1. At the highest level we will make sure that all ArgoCD self-management resources are deployed first. They will get number "-12" to "-10"
2. Then our infrastructure tools will be deployed (observability, service-mesh, etc.). They will get numbers "-5" to "-1".
3. My-app resources come next. Backend will get "0" and Frontend "1".
4. Within Backend and Frontend, the individual manifest also get Sync Waves. These sync wave numbers will be evaluated within the scope of the Application in which they are deployed, so they will not compete with the numbers assigned to, for example, the Prometheus Application.

**IMPORTANT**:<br>
- I chose these numbers arbitrarily, feel free to change them or raise an issue if you see room for improvement.
- By default ArgoCD is not able to apply Sync Waves for manifests of type Application. I had to do [this](https://argo-cd.readthedocs.io/en/stable/operator-manual/upgrading/1.7-1.8/#health-assessment-of-argoprojioapplication-crd-has-been-removed) to make it work. You can see it in the [ArgoCD Helm chart custom values file](/helm-charts/infra/argo-cd/values-custom.yaml).
- Before running the Destroy All The Things pipeline, make sure all applications are healthy, the implementation of Sync Waves will mess with applications deletion if they are not healthy.

Here are the specific numbers:

## ArgoCD Self-Manage Applications
- -12 ArgoCD AppProjects (ArgoCD Projects)
- -11 ArgoCD (ArgoCD itself)
- -10 ArgoCD Apps (App of Apps)

## App of Apps
- -5 Prometheus
- -4 Istio Base / Jaegger / Loki / Sealed-Secrets
- -3 Istiod / Grafana 
- -2 Istio Gateway / Flagger
- -1 Kiali / Flagger Load-Tester / Backstage
- 0 Backends
- 1 Frontends

## Backend Applications
- -1 Sealed-Secret
- 0 Deployment
- 1 Canary

## Frontend Applications
- 0 Deployment
- 1 Canary

<br/>
<br/>
<p title="Kill chain" align="center"> <img width="460" src="https://i.imgur.com/KcSXPER.jpg"> </p><br/><br/><br/>
<br/>
<br/>

# ARGOCD DEPLOYMENT PIPELINE

## Description

We won't go into what ArgoCD is, for that you have [this video](https://youtu.be/MeU5_k9ssrs) by the #1 DevOps youtuber, Nana from [TechWorld with Nana](https://www.youtube.com/@TechWorldwithNana).

This pipeline will use the [ArgoCD Helm Chart](/helm-charts/infra/argo-cd/) in our repo to deploy ArgoCD into our EKS.<br>
The first thing it will do is run the necessary tasks to connect to our the cluster. After this, ArgoCD will be installed, along with its Ingress.

It will then create the necessary resources for ArgoCD to be self-managed and to apply the [App of Apps pattern](https://youtu.be/2pvGL0zqf9o). ArgoCD will be watching the helm charts in the [helm-charts](/helm-charts) directory in our repo, it will automatically create all the resources it finds and apply any future changes me make there. The [helm-charts/infra](/helm-charts/systems/my-app) and [helm-charts/systems/my-app](/helm-charts/systems/my-app) directories simulate what would be our K8S infrastructure repositories would be.

If you want to know more about Helm, [here's another Nana video](https://youtu.be/-ykwb1d0DXU).

Following up, it will get the Istio Gateway endpoint and put it into the [frontend values file](/helm-charts/systems/my-app/frontend/values.yaml). It will also export the endpoint for each environment as an artifact.

Finally the pipeline will get the ArgoCD web UI URL and admin account password and export them as an artifact too. You might need to wait a few seconds for the URL to be active, this is because an AWS Load Balancer takes a little time to be deployed.

<br/>

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "02-Deploy ArgoCD" workflow.
3. Click on "Run workflow" (Use workflow from Branch: main).
4. When it's finished, the frontend endpoints and ArgoCD access files will be exported as artifacts. You'll find them in the workflow run screen under "Artifacts". Download them to see the ArgoCD URL and credentials, and the frontend endpoints.
5. You can now access the ArgoCD UI, if it's not ready just hit refresh every few seconds.

<br/>
<br/>
<p title="Gitops Chills" align="center"> <img width="460" src="https://i.imgur.com/kGQUUTw.jpg"> </p>
<br/>
<br/>


# SEALED SECRETS PIPELINE

## Description

Up until now, we have been leaving our Kubernetes secrtes exposed in our repo. Anyone with access to the repo could see the what the password for the Redis DBs were. Technically, they were base64 encoded, but anyone could easily decode them.

From now on, we will encrypt them, and for this we will use Bitnami Sealed Secrets. As always, I'm not going into details on how the tool works, but you can check out [this video](https://youtu.be/wWMJCY2E0d4?si=zX93I7hji-6w7hnX) from KodeKloud.

You could easily encrypt the secrets yourselves using the kubeseal CLI tool, but I made a pipeline to make it easier. Before running, the pipeline will require you to introduce the Redis passwords for each environment. The pipeline will then install the Kubeseal CLI tool and with it, it will generate Sealed Secrets and save the values of the encrypted passwords to the [values files of each environment](/helm-charts/systems/my-app/backend/environments/). The [sealed secret manifest](/helm-charts/systems/my-app/backend/templates/redis-sealed-secret.yaml) will use these values to create the SealedSecret objects in the cluster.

Same will be done for the GitHub token secret that Backstage will use.

<br/>

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "03-Sealed secret generator" workflow.
3. Click on "Run workflow".
4. Complete the empty fields. Passwords are:
- automate-all-the-things-dev
- automate-all-the-things-stage
- automate-all-the-things-prod
5. Click on "Run workflow".


<br/>
<br/>
<p title="Keep your secrets" align="center"> <img width="460" src="https://i.imgur.com/rmhp3EJ.jpg"> </p>
<br/>
<br/>


<!-- # BACKEND SERVICE BUILD & DEPLOY PIPELINE

## Description

Our app is made of two microservices (backend and frontend) and a database. Let's start with the backend.

The [application-code/my-app/backend directory](/application-code/my-app/backend) on the repo is meant to represent the backend microservice application code repository. Here you'll find the code files and the corresponding Dockerfile for the backend service.

There's four stages on this pipeline:

On the Build stage we will use Docker to build a container image from the Dockerfile, tag it with the number of the pipeline run and push it to your DockerHub registry.

On the Deploy Dev stage, we will checkout the repo and modify the [helm-charts/systems/my-app/backend/environments/values-dev.yaml file](/helm-charts/systems/my-app/backend/environments/values-dev.yaml) and push the change to GitHub. [But why?](https://i.gifer.com/2Gg.gif)<br>
Remember how we just pushed the image to DockerHub with the new tag? And remember how ArgoCD is watching the helm/my-app directory? Well, this is how we tell ArgoCD that a new version of the backend microservice is available and should be deployed. We modify the image.tag value in the values-dev.yaml file and wait for ArgoCD to apply the changes.

[This is how gentlemen manage their K8S resources](https://i.imgur.com/2Xntz2P.jpg). We are not some cavemen creating and deleting stuff manually with kubectl. We manage our infrastructure with **GitOps**.

After the Deploy Dev stage is done, and only if it was successful, the Deploy Stage stage will commence. It will do the same thing as the previous stage, but this time modifying the [helm-charts/systems/my-app/backend/environments/values-stage.yaml file](/helm-charts/systems/my-app/backend/environments/values-stage.yaml).

We'll repeat the same process for Prod, but since Prod should be a more delicate environment, the Deploy Prod stage will require authorization from the top level excecutives (in this case it's you, congrats boss) to be executed. You'll receive an email with a link asking you to verify and approve the deployment to Prod. Go ahead and approve it.

That's it! Your app was deployed to all environments! Good job buddy!

This pipeline is automatically triggered everytime there are any changes commited inside the "backend service application code repository" (meaning the [pplication-code/my-app/backend directory](/application-code/my-app/backend)). In this manner, if the backend developers commit any changes to the backend service, they will be automatically built and deployed to the cluster. That's some delicious CI/CD for you baby.

Now, if the infrastrucure team needs to make changes to the cluster resources, they would work on the "K8S infrastructure repository" (meaning the [helm-charts/systems/my-app directory](/helm-charts/systems/my-app)). Let's say they need to increase the number of pod replicas for the backend service in the prod environment, then they'd change the value of deployment.replicas in the [helm-charts/systems/my-app/backend/environments/values-prod.yaml file](/helm-charts/systems/my-app/backend/environments/values-prod.yaml), commit the change and wait for ArgoCD to apply the changes on the cluster. There's some tasty Gitops for you too.

<br/>

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "04-Build & deploy my-app-backend image" workflow.
3. Click on "Run workflow" (Use workflow from Branch: main).

<br/>
<br/>
<p title="Momoa & Cavill" align="center"> <img width="460" src="https://i.imgur.com/pCjM1d6.jpg"> </p>
<br/>
<br/>

# FRONTEND SERVICE BUILD & DEPLOY PIPELINE

## Description

The [application-code/my-app/frontend directory](/application-code/my-app/frontend/) on the repo is meant to represent the frontend microservice code repository. Here you'll find the code files and the corresponding Dockerfile for the frontend service.

Just as in the backend pipeline, there's four stages on this pipeline:

1. We build and push our frontend image to DockerHub.
2. We deploy to Dev environment in the same manner we did with the backend (modifying the image.tag value in the [helm-charts/systems/my-app/frontend/environments/values-dev.yaml file](/helm-charts/systems/my-app/frontend/environments/values-dev.yaml)).
3. If deployment to Dev was OK, we deploy to Stage.
4. If deployment to Stage was OK, we'll get an email requesting authorization for deployment to Prod. Give it the thumbs up and our app will be deployed to Prod.

That's it! Your entire app was deployed to all environments! Good job buddy!

Just as with the backend, this pipeline is automatically triggered everytime there are any changes commited inside the "frontend service application code repository" (meaning the [application-code/my-app/frontend directory](/application-code/my-app/frontend/)). In this manner, if the frontend developers commit any changes to the frontend service, they will be automatically built and deployed to the cluster.

For the infrastructure, same as before. If the infrastrucure team needs to, for example, change the number of pod replicas for the frontend service in the dev environment, then they'd change the value of deployment.replicas in the [helm-charts/systems/my-app/frontend/environments/values-dev.yaml file](/helm-charts/systems/my-app/frontend/environments/values-dev.yaml), commit the change and wait for ArgoCD to apply the changes on the cluster.

<br/>

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "05-Build & deploy my-app-frontend image" workflow.
3. Click on "Run workflow" (Use workflow from Branch: main).

<!-- 9. When it's done, you should be able to access the URLs you got from the ArgoCD Deployment pipeline. But if you go to the URLs too quickly you'll see nothing there. We need to give ArgoCD a little time to notice the changes in the [/helm/my-app/frontend directory](helm/my-app/frontend). By default ArgoCD pulls for changes every three minutes. You can either wait like an adult or go into the ArgoCD web UI and hit "Refresh Apps" like the impatient child that you are.
11. Check the URLs again.
12. On the top left of the website you'll see the "Visit count". This number is being stored in the ElatiCache DB and accessed through the backend.
13. Hope you like the web I made for you. If you did, go leave a star on [my repo](https://github.com/tferrari92/automate-all-the-things-insane). -->

<br/>
<br/>
<p title="Anakin" align="center"> <img width="460" src="https://i.imgur.com/V1qgXKM.jpg"> </p>
<br/>
<br/> -->


# KUBERNETES TOOLS MANAGEMENT

## Description

Let's talk how we're meant to manage the installation, customization and uninstallation of Kubernetes tools from now on.

If you haven't figured it out yet, let me explain how the system works:<br>
ArgoCD has an Application running which watches the [argo-cd/applications directory](/argo-cd/applications). It will deploy all application.yaml's it finds there. Each of these application.yaml's point to their corresponding Helm chart in the [helm directory](/helm-charts). This is know as the App of Apps pattern.<br>
When we want to add a new Kubernetes tool to our cluster (let's use Jenkins as an example), we'll do the following:

<br/>

## Instructions

1. Download the Helm chart: after you added the repo, use this command:
```bash
helm pull jenkinsci/jenkins --untar
```
2. Copy the chart to the [helm-charts/infra directory](/helm-charts/infra).
3. Create a values-custom.yaml where we'll specify our custom values. We NEVER touch the original values file, we want to have a clear distinction between default configuration and custom configuration.
4. If we need to add a new manifest, we'll create a directory called custom-templates inside the templates directory in the chart and drop our custom manifest in there. 
5. Our chart is ready. We'll now create an application.yaml for it.
6. Copy any of the existing application.yamls and make the required changes. These changes will be on metadata.name, spec.source.path and, depending on what you are deploying, also on spec.destination.namespace and spec.project.
7. Save this new application.yaml in the [argo-cd/applications/infra directory](argo-cd/applications/infra).

That's it! Now you just need to wait. When Argo sees the new application.yaml it will deploy it automatically.<br>
If you need to make any further customizations to the chart, you can modify the values-custom.yaml or the contents of the custom-templates directory.<br>
If you want to remove the tool from your cluster, [just delete the application.yaml you created and wait](https://i.imgur.com/KcSXPER.jpg).

We can follow this same logic for deploying new my-app services, for example for a second backend.

<br/>
<br/>
<p title="Two buttons" align="center"> <img width="460" src="https://i.imgur.com/Fgo7nnZ.jpg"> </p>
<br/>
<br/>

# DESTROY ALL THE THINGS PIPELINE

## Description

Let's burn it all to the ground.

Remember how the AWS Load Balancer Controller created this problem for us where some Applications Load Balancers were created automatically in AWS but were not tracked by our Terraform? Well, in this pipeline, the first thing we need to do it take care of this.

The pipeline will first eliminate ArgoCD from our cluster and then delete all Ingress  and Persistent Volume resources. This will automatically get rid of any Application Load Balancers and EBS volumes in AWS.

After this, the pipeline will be able to run "terraform destroy" with no issues. Our infra will be obliterated and we won't be giving any more of our precious money to Bezos.

The pipeline will finish with a warning, worry not, this is because the "terraform destroy" command will have also deleted our terraform backend (the Bucket and DyamoDB Table), so Terraform won't be able to push the updated state back there. We can ignore this warning. I wish there was a more elegant way of finishing the project but I couldn't find any so deal with it.

## Instructions

1. On your GitHub repo, go to the "Actions" tab.
2. Click on the "06-Destroy infrastructure" workflow.
3. Click on "Run workflow" (Use workflow from Branch: main).
4. There's two AWS resources that for some reason don't get destroyed: a DHCP Option Set and an Auto Scaling Managed Rule. I'm pretty sure these don't generate any expenses but you can go and delete them manually just in case. I'm really sorry about this... I have brought [shame](https://i.imgur.com/PIm1apF.gifv) upon my family...

<br/>
<br/>
<p title="Seagull" align="center"> <img width="460" src="https://i.imgur.com/2Z8qEvC.png"> </p>
<br/>
<br/>

---

<br/>

# CONCLUSION

Our journey comes to an end... Congratulations! You made it!

I hope this proved useful (and fun), that you learned something and that you can take some pieces of this to use in your own projects.

You now possess the power of of CI/CD, GitOps, and Infrastructure as Code. You know what [this means](https://www.youtube.com/watch?v=b23wrRfy7SM), use it carefully.

<br/>
<p title="Thanos" align="center"> <img width="500" src="https://i.imgur.com/dgB9Olt.jpg"> </p>
<br/>
<br/>

Special thanks to all these wonderful YouTube people. This wouldn't have been possible without them:

- Nana Janashia from [Techworld With Nana](https://www.youtube.com/@TechWorldwithNana)
- Viktor Farcic from [DevOps Toolkit](https://www.youtube.com/@DevOpsToolkit)
- Marcer Dempers from [That DevOps Guy](https://www.youtube.com/@MarcelDempers)
- Sid Palas from [DevOps Directive](https://www.youtube.com/@DevOpsDirective)
- Mumshad Mannambeth and his guys from [KodeKloud](https://www.youtube.com/@KodeKloud)
- [Anton Putra](https://www.youtube.com/@AntonPutra)

### Happy automating!

<br/>

## On the next edition

[Automate All The Things Nirvana Edition](https://github.com/tferrari92/automate-all-the-things-nirvana):

- We'll start using Horizontal Pod Autoscalers.
- We'll automate TLS certificates provisioning with Kubernetes Cert Manager.
- We'll automate DNS records provisioning with Kubernetes External DNS.
- We'll ditch DockerHub and start using our self-hosted image registry with Harbor.
