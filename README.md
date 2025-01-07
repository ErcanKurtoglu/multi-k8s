# Multi-Container App with Kubernetes on GKE
This project was created to implement Kubernetes applications with multi-containers. A React app and Fibonacci sequence calculation algorithm were developed and deployed on GKE. (It was prepared as a continuation of the Multi-Docker ElasticBeanstalk project. The project architecture is listed in the Project Structure section.)

CI/CD processes were managed using Github Actions.

The application is accessible via the domain names `ercankurtoglu.xyz` and `www.ercankurtoglu.xyz`, and HTTPS certificate settings have been configured.

On the website interface, users can enter a desired number, click the `Submit` button, and the page refreshes to display the result in the list below.

*<u>Note:</u> Using GCP (Google Cloud Platform) may incur costs.*

## Important Links
* [WSL2](https://learn.microsoft.com/en-us/windows/wsl/about): The entire project was developed on WSL (Windows Subsystem for Linux).
* [Docker Desktop](https://www.docker.com/products/docker-desktop): Used to create container applications with WSL2 and as a VM for Kubernetes.
* [Docker Hub](https://hub.docker.com/): For using pre-built services and pushing project-specific services.
* [GCP](https://console.cloud.google.com): The platform where the project was deployed using Google Kubernetes Engine (GKE).
* [Github Actions](https://github.com/ErcanKurtoglu/multi-k8s/actions): The platform for managing the CI/CD pipeline of the project.
* [Ingress-nginx](https://github.com/kubernetes/ingress-nginx): Configured ingress to route incoming traffic in the Kubernetes project. [Kubernetes Deployment Page for installing ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/).  
  Extra reading: [Studying the Kubernetes Ingress System](https://www.joyfulbikeshedding.com/blog/2018-03-26-studying-the-kubernetes-ingress-system.html).

## Contents of this Page
- [Project Materials](#project-materials)
- [Project Structure](#project-structure)

## Project Materials
This table contains necessary explanations and links related to the files.

## Folder Tree:
![alt text](slides/img/{2B49491B-0FAD-4602-9259-48A0542DB1F9}.png)

| Number | Title | File | Description | Slides |
| -- | -- | -- | -- | -- |
| 00 | [React Server](#-00-react-server) | [Folder:client](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/client) | Created using React app | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/00_reactserver.pdf) |
| 01 | [Express Server](#-01-express-server) | [Folder:server](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/server) | Source managing the data flow with Express server | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/01_expressserver.pdf) |
| 02 | [Fibonacci](#-02-fibonacci) | [Folder:worker](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/worker) | Source running the Fibonacci algorithm | |
| 03 | [Kubernetes](#-03-kubernetes) | [Folder:k8s](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/k8s) | Contains Kubernetes configuration files | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/03_kubernetes.pdf) |
| 04 | [Github Actions](#-04-github-actions) | [Folder:.github/workflows](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/.github/workflows) | YAML file for CI/CD via Github Actions | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/04_githubactions.pdf) |
| 05 | Github Actions Secret, Repo Secret |  | Encrypting GKE user secret file and adding repository secrets | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/05_secrets.pdf) |
| 06 | GCP |  | Creating a Kubernetes cluster on GCP and setting necessary configurations. DNS setup for domain names if needed. | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/06_gpc.pdf) |


## Project Structure
The services, pods, and clusters created in this project are illustrated schematically, and the required schemas can be accessed via the links in the table below.

General project architecture:  
![alt text](slides/img/{24690D01-2BFD-443F-BB16-A770D9A86748}.png)

| File | Description | Schema |
| -- | -- | -- |
| Old system architecture (Docker Container) | This project was previously prepared for deployment on AWS EBS using Travis-ci CI/CD with Docker Container. | [Goto Schema](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/old_system.pdf) |
| Project architecture | Multi-docker images were created and configured easily using Kubernetes. Nodes were created using object types like Ingress-nginx, Deployment, ClusterIP, and PVC. | [Goto Schema](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/project_architecture.pdf) |

### 🔐 00. React Server

1. <u>Downloaded Node.js:</u>  

    Node.js was installed for Linux using `nvm` as the project was developed on a WSL system.  
    [Download Node.js](https://nodejs.org/en/download)

    ![alt text](slides/img/{95DDBAEA-E7A5-4F76-B917-16FC328E39A8}.png)

2. <u>Created React app:</u>  

        npx create-react-app client

3. <u>Added Fib.js and Other.js:</u>  

    **Fib.js:** A page where the Fibonacci algorithm is executed. Users can input values to see the result, and all entered values are displayed on this page.  
    **Other.js:** An empty page.

### ![alt text](slides/img/o46jvwuf2.png) 01. Express Server
The Express Server acts as a communication bridge between Redis, Postgres, and the React App.

### ![alt text](slides/img/dhtnoalh.png) 02. Fibonacci
A server where the Fibonacci algorithm is executed. The application displays Fibonacci numbers up to 40.

### ![alt text](slides/img/260p99kt2.png) 03. Kubernetes
For both client and server services, 3 pods were created each, while other services have 1 pod each. Each service has a ClusterIP Service. Ingress-Nginx is configured for the entry traffic to the node.

For local development, use the [ingress-service-local-dev](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/k8s_local_dev/ingress-service-local-dev.yaml) configuration file. Certificate, issuer, and ingress-service configuration files should not be used. Additionally, other configuration files inside the `k8s` folder should be applied.

Local development:  

    kubectl apply -f [yaml files]

For production, use the opposite configuration files. Necessary production setup is included in the Github Actions configuration file.

### ![alt text](slides/img/fpa0rfwt2.png) 04. Github Actions

Github Actions is where the CI/CD processes are managed. All operations are executed in two jobs: testing and deployment. Each pull request (PR) triggers the process, and automated tests are performed. If the tests pass successfully, automatic deployment is executed.

### ![alt text](slides/img/u7q072ec2.png) 05. Secrets

Sensitive data for the project is stored here. To add new secrets:  

    [Repo] -> Settings -> Secrets and variables -> Action -> New Repository secret

### ![alt text](slides/img/podz7i7h2.png) 06. GCP

The project was deployed on GCP.  
* After logging in, create a new project.  
* Link the project to a `Billing account`.  
* Configure necessary settings via Shell.  
* Create a secret for `Postgres` using Shell.  
* Create an `ingress-nginx controller` via Shell.  
* Create a `cert-manager` via Shell (for HTTPS certificates).  
* Configure DNS settings (if domain assignment is required).  

**Detailed steps can be found in the relevant slide document.**

<u>**Clean-up: Project -> Click gear icon -> Select project -> Delete**</u>
