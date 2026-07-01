# DevOps & Cloud Fundamentals

## DevOps

DevOps is a cultural & technical approach that integrates development &
operations teams to deliver software in a faster, more reliable & automated way.

In a traditional setup, code may work on a developer's machine but fail in
production due to differences in environments or deployment processes. DevOps
solves this by standardizing environments & introducing automation through
CI/CD pipelines, where code is automatically built, tested & validated before
deployment.

Moreover, applications are packaged using containers like Docker to ensure
consistency across environments & deployed on orchestration platforms like
Kubernetes, which handle scaling, load balancing etc. Along with this,
monitoring & logging systems provide real-time visibility into application
performance & failures.

Overall, DevOps enables a strong feedback loop between dev, operations &
production systems, allowing teams to release features faster with higher
reliability, fewer manual errors & better system stability at scale.

---

## SDLC

SDLC stands for **Software Development Life Cycle**. It is the process of
developing software from start to finish. The main phases are:

- Requirement Gathering
- Planning
- Design
- Development
- Testing
- Deployment
- Maintenance

Common SDLC models include: **Waterfall, Agile, Spiral, V-Model & Iterative**.

Today, Agile is the most widely used because it delivers software in small
regular updates & can easily handle changing requirements.

---

## Cloud Computing

**Cloud computing** is the delivery of computing services like servers, storage,
databases, networking & software over the internet on a pay-as-you-go basis.

**Server** is a computer that provides services or resources to other computers.

**Virtual Machine (VM)** is a software-based computer that runs like a physical
computer, where we can install an operating system & run applications.

---

## Cloud Concepts

| Concept | Definition |
|---|---|
| **Region** | A geographical area where a cloud provider has data centres |
| **Availability Zone** | An isolated data centre within a region that helps improve availability & fault tolerance |
| **Public Cloud** | A shared infrastructure managed by the provider |
| **Private Cloud** | A dedicated infrastructure for one organization |
| **Auto Scaling** | A technology which automatically adds or removes servers based on application demand |
| **Load Balancer** | Distributes incoming traffic across multiple servers to improve performance & reliability |
| **VPC** | A private network in the cloud where resources like VMs, databases & applications are securely placed |

---

## Cloud Service Models

### IaaS — Infrastructure as a Service
The cloud provider gives us virtual machines (EC2 in AWS), storage &
networking, while we manage the operating systems & applications.
> Ex: EC2 in AWS

### PaaS — Platform as a Service
The provider manages the infrastructure & operating system, & we only develop
& deploy our applications.
> Ex: AWS Elastic Beanstalk

### SaaS — Software as a Service
The provider manages everything & users can simply access the software through
the internet.
> Ex: Gmail, Microsoft 365, Zoom
