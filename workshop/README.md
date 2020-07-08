
## App Modernization Workshop

In the workshop you will learn about foundational open source technologies and industry-wide accepted best practices for building modern, scalable, portable, and robust applications. You will learn migration strategies for moving legacy, monolithic WAS applications into Liberty containers running on Red Hat OpenShift, and some of the common pitfalls to watch out for.

- [App Modernization Workshop](#app-modernization-workshop)
- [Lab Setup](#lab-setup)
- [Day 1](#day-1)
- [Day 2](#day-2)
- [Day 3](#day-3)
- [Technology Used](#technology-used)
- [Presenters](#presenters)

## Lab Setup 
|   |   |
| - | - |
| [Cloud Workshop + Cloud Shell Setup Instructions](pre-work/CloudWorkshopK8sWithWebTerminal.md) | Run these steps to setup your environment for the labs

## Day 1
|  Topic | Description  |
| - | - |
| Welcome, Introductions, Objectives and Setup| - |
| [Lecture: Overview of Docker](https://ibm.box.com/s/0mvlb8hvd8lx23smfvoaijdt9ex63go2)|  |
| [Lecture: Overview of Kubernetes](https://ibm.box.com/s/p8jqmihxterlpsrvg5d35yihs0am4c8g) |  |
| BREAK | |
| [Lab: Kubernetes 101](generatedContent/kube101/README.md) | Deploying, Scaling, and Operators |
| LUNCH	| |	
| [Lecture: Helm](https://ibm.box.com/s/cluclg99642s5bgi6j2wixr37jg7nw96) | Helm Overview Lecture |
| [Lab: Helm](generatedContent/helm101/README.md) | Series of Helm Labs 
| RECAP and Survey | |

** Install helm v3**
```
curl -LO https://raw.githubusercontent.com/remkohdev/setup/master/install-helm.sh
chmod 755 install-helm.sh
./install-helm.sh
helm version --short
```

## Day 2
|  Topic | Description  |
| - | - |
| Welcome, Day 1 Recap / Questions | |
| [Lecture: Istio](https://ibm.box.com/s/4al8hgpzj90vuus55i9fmcw856qz1bt1) | Overview of Istio Service Mesh |
| [Lab: Istio](istio101/setup.md) | Working with Istio (Deploying Applications and Traffic Management)
| BREAK | |
| [Lab: Add Secure Object Storage to MongoDB](generatedContent/ddc-cloud-native-security-labs.git/lab-02/README.md)	| |
| LUNCH | |
| [Lecture: Overview of Kubernetes Extensions](https://ibm.box.com/s/c7r9vsfdqtev76p1nqvdvumnoc6cai7m) | |
| [Lab: Custom Resources and Operators](generatedContent/kubernetes-extensions.git/README.md) | |
| RECAP and Survey | |

**Install helm v3**
```
curl -LO https://raw.githubusercontent.com/remkohdev/setup/master/install-helm.sh
chmod 755 install-helm.sh
./install-helm.sh
helm version --short
```

**Install Go**
```
curl -LO https://golang.org/dl/go1.14.4.linux-amd64.tar.gz 
tar -C /usr/local -xzf go1.14.4.linux-amd64.tar.gz 
export PATH=$PATH:/usr/local/go/bin
go version
```

**Install the Operator SDK**
```
curl -LO https://github.com/operator-framework/operator-sdk/releases/download/v0.18.2/operator-sdk-v0.18.2-x86_64-linux-gnu 
chmod +x operator-sdk-v0.18.2-x86_64-linux-gnu 
sudo mkdir -p /usr/local/bin/ 
sudo cp operator-sdk-v0.18.2-x86_64-linux-gnu /usr/local/bin/operator-sdk 
rm operator-sdk-v0.18.2-x86_64-linux-gnu
operator-sdk version
```

## Day 3
|  Topic | Description  |
| - | - |
| Welcome, Day 2 Recap / Questions | |
| [Overview of CI/CD for Microservices](https://ibm.box.com/s/8y9yglljd4yd7xmdo501o1xyqta3p9q9)	| |
| [Lab: Source-to-Image (S2I)](generatedContent/ddc-cloud-native-security-labs.git/lab-03/README.md) | S2I with Custom Builder and Runtime Image
| BREAK | |
| [Lecture: Overview of Tekton Pipelines](https://ibm.box.com/s/kisshn88w4a79jzz557o5h6c5k55o9ze) | Tekton Overview Lecture|
| [Lab: Tekton on OpenShift](generatedContent/tekton-tutorial-openshift/README.md) | Tekton Pipelines in OpenShift Lab
| LUNCH | |
| Overview of Multi-Cloud Management and Policy Governance by Greg | |
| RECAP and Survey | |

## Technology Used

* Docker
* Kubernetes
* Helm
* RedHat OpenShift
* IBM Kubernetes Service
* Istio


## Presenters

* [Remko de Knikker](https://github.com/remkohdev)
* [John Zaccone](https://github.com/jzaccone)

