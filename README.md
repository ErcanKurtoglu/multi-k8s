# Multi Container App with Kubernetes on GKE
Bu proje multi-containerlar ile kubernetes uygulaması yapmak amacıyla hazırlanmıştır. React app ve Fibonacci serislerini hesaplama algoritması oluşturularak GKE 'de deploy edilmiştir. (Multi-Docker ElasticBeanstalk projesinin devamı olarak hazırlanmmıştır. Proje mimarisi Project Structure bölümünde listelenmiştir.)

## Important links
* [WSL2](https://learn.microsoft.com/en-us/windows/wsl/about): Bütün proje WSL'de (Windows Subsystem for Linux) hazırlanmıştır.
* [Docker-desktop](https://www.docker.com/products/docker-desktop/): WSL2 ile container ugulamaların oluşturulması ve Kubernetes için VM olarak kullanılması.
* [Docker-hub](https://hub.docker.com/): Hazır servislerin kullanılması ve projede oluşturulan servislerin pushlanması.
* [GCP](https://console.cloud.google.com): Google Cloud Platform ve Google Kubernetes Engine (GKE) projenin deploy edildiği platform.
* [Github Actions](https://github.com/ErcanKurtoglu/multi-k8s/actions): Projenin CI/CD sinin yapıldığı platform.
* [Ingress-nginx](https://github.com/kubernetes/ingress-nginx): Kubernetes projemizde gelen trafiği yönlendirmesi için ingress configurasyonun yapılması. [Kubernetes Deployment Page for intalling ingress controller](https://kubernetes.github.io/ingress-nginx/deploy/) Extra reading: https://www.joyfulbikeshedding.com/blog/2018-03-26-studying-the-kubernetes-ingress-system.html



## Contents of this page
- [Project Metarials](https://github.com/ErcanKurtoglu/multi-k8s#project-metarials)
- [Project Structure](https://github.com/ErcanKurtoglu/multi-k8s#project-structure)

## Project Metarials

Bu tablo dosyalarla ilgili gerekli açılamaları ve linkleri içermektedir.
 
## Folder tree:

![alt text](slides/img/{366B27B4-1200-4B54-BD17-EE12EF0FA03E}.png)

| Number | Title | File | Description | Slides |
| -- | -- | -- | -- | -- |
| 00 | [React Server](https://github.com/ErcanKurtoglu/multi-k8s#00-react-server) | [Folder:client](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/client) | React app ile oluşturuldu | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/slides/00_reactserver.pdf) |
| 01 | Github Actions Secret | [service-account.json.gpg](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/service-account.json.gpg) | GKE user secret file | [Goto Slide](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/service-account.json.gpg) |
|----|----|----|

## Project Structure
Bu projede hazırlanan serviceler, podlar, clusterlar şematik olarak gösterilmiştir ve gerekli şemalara tablodaki linklerden ulaşılabilir.

| File | Description | Schema |
| -- | -- | -- |
| [Old system architecture(Docker Container)](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/service-account.json.gpg) | Bu proje daha önce Docker Container kullanılarak AWS üzerinden EBS ile deploy edilmek üzere hazırlanmıştır. Temal mimari şeması => | [Goto Schema](https://github.com/ErcanKurtoglu/multi-k8s/blob/master/slides/service-account.json.gpg) |
|----|----|----|

### 🔐 00. React Server






-Root
  -client
  -server
  -worker
  -k8s