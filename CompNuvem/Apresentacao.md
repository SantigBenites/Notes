# Introduction

The DevSecOps paradigm is a subsection of DevOps, which integrates secure software practices into the development and production environments. However, companies may be misled into thinking they have solved their security issues by merely adopting DevSecOps without additional input. This paper presents a case study of a DevOps pipeline, including GitHub, Jenkins, DockerHub, and K8s components, to demonstrate potential security threats and vulnerabilities. Four attack scenarios were developed, and mitigation techniques were proposed. The study highlights the need to raise awareness of the importance of securing DevOps pipelines and preventing insecure software supply chain systems.

# Setup

A system was created to demonstrate the use of a SSCS(software supply chain system) to integrate and deploy a secure application as an insecure software. The system uses a web application developed in Python utilizing Flask and uses Apache Kafka to interact with Strimzi. The application components are deployed to Kubernetes, an orchestration tool for Docker containers, and Jenkins is used for Continuos Integration / Continuos Deployment.

# Attack types

4 main attack types were derived, based on their inputs and outputs.

## Retrieve Information in Topic

Attack 1
The goal of the attack is to compromise information from secure applications inside the K8s cluster.
This attack deals with an attacker having privileges to deploy containers into the K8s cluster.
This is usually not possible considering the data is only available through the K8s DNS service, to this effect the attacker deploys a custom application which will provide a front facing UI.
The attacker can after connect to the UI to use the app as an entry point into the cluster allowing it to siphon data from Strimzi and the cluster.

## Manipulate Continuos Integration / Continuos Deployment by Modifying the Files

Attack 2
This attack deals with an attacker having privileges to the Jenkins instance serving the Continuos Integration / Continuos Deployment
To this effect the attacker selects a build step and modifies the files before packaging and deployment.
After modified, anything can trigger the malicious payload inserted by modifying the files, which will allow the attacker to have full access to the system.
Depending on the scope of the application this vulnerability can attack multiple systems.

## Kubernetes Expose clusterIP to External Users

Attack 3
This attack deals with an attacker that has access to the K8s cluster networking protocols.
To this effect the attacker uses another ingress object, this object will serve as an entrypoint for the cluster and allows the attacker to communicate with the internal ports of the cluster.
This in it self allows access from external applications to the applications inside the cluster, granting access to a possibly vulnerable application which can lead to leaks of vulnerable data

## Kubernetes hostPath Namespace Breakout

Attack 4
The final attack involves exploiting the hostPath volume to mount an escape for privilege escalation in a K8s namespace. An attacker can deploy a malicious pod with hostPath access, change root to access the root file system, and gain cluster admin privileges to target secure applications and perform malicious actions such as editing or deletion. The attack can be performed with the help of a service account with CRUD privileges in any namespace.

# Protection mechanisms

To prevent these attacks the authours present some protection mechanisms.
The common theme amongst all these attacks is privilege escalation, therefore it stand to reason that the solution will be better implementation of principle of least privilege when managing a SSCS(software supply chain system) within the utilized DevSecOps model K8s.
Specifically each attack can be solved by using:

## Protection from deploying malicious application

For attack 1 the main protection is limiting user privileges, this can be done by implementing service accounts that are tied to specific namespaces to prevent users from deploying containers outside their dedicated area.

## Protection from the CI/CD manipulation

For attack2 the main protection is restricting access to Jenkins instance, this can be implemented with the usage of a service account to trigger the Jenkins job and limit other uses to the admin.

## Cluster IP exposure mitigation

For attack 3 the main protection is to establish service accounts in the K8s cluster, assigning specific service accounts to access specific resources within certain namespaces.

## HostPath volume escalation mitigation
For attack 4 the main protection from the hostPath volume namespace breakout is to restrict the CRUD privileges to higher level accounts, and if lower level accounts that needs CRUD privileges must authenticate as a high level user to perform their tasks.
Another recommendation is to acquire dedicated storage so to prevent the need of hostPath volumes being deployed.
