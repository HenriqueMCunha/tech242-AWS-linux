# CI / CD
- [CI / CD](#ci--cd)
  - [Continuous Integration](#continuous-integration)
  - [Continuous Delivery](#continuous-delivery)
  - [Continuous Deployment](#continuous-deployment)
  - [Differences between Continuous Delivery and Continuous Deployment](#differences-between-continuous-delivery-and-continuous-deployment)
  - [Jenkins](#jenkins)
    - [Benefits](#benefits)
    - [Disadvantages](#disadvantages)
    - [Stages of Jenkins](#stages-of-jenkins)
    - [Alternatives to Jenkins](#alternatives-to-jenkins)
    - [Why is it referred as a Pipeline?](#why-is-it-referred-as-a-pipeline)
    - [Why build a Pipeline?](#why-build-a-pipeline)
  - [Building a CI / CD pipeline with Jenkins](#building-a-ci--cd-pipeline-with-jenkins)
    - [Notes to integrate further](#notes-to-integrate-further)

CI / CD is essentially a set of practices:
* Continuous Integration
* Continuous Delivery/Deployment

## Continuous Integration

* Continuous Integration (CI) is a development practice where developers regularly integrate their code changes into a shared repository. Each integration triggers automated builds and tests, ensuring early detection of integration issues and promoting a more collaborative and efficient development process.
* Imagine merging tiny code changes frequently into a shared repository, followed by automated builds, tests, and feedback. 

## Continuous Delivery

* Continuous Delivery (CD) is an extension of CI by automatically deploying code changes to testing or staging environments after successful builds. It aims to make the delivery process more reliable and faster, allowing teams to release software more frequently and with greater confidence.
* This allows for faster deployments and smoother releases.
* What is delivered?
  * Ready to be deployed code.
  * Will create artifacts (e.g. jar file in java)

## Continuous Deployment

Continuous deployment is a strategy in software development where code changes to an application are released automatically into the production environment.
* It's faster for end users.
* There's continuous feedback from end users to developers)

![diagram-ci-cd.png](../../readme-images/diagram-ci-cd.png)

## Differences between Continuous Delivery and Continuous Deployment

* Continuous Deployment (CDE): Involves automatically deploying code changes directly to production after successful testing, with minimal manual intervention.

* Continuous Delivery (CD): Focuses on automatically delivering code changes to non-production environments, leaving the decision to deploy to production to a manual trigger.

* We can think of it like this: CD builds a bridge between our code and various environments, while CDE pushes changes directly to production, like a highway with no exits. Both offer speed and efficiency, but CDE demands stricter quality control.

![diagram-cd-vs-cde.png)](../../readme-images/diagram-cd-vs-cde.png)

## Jenkins

Jenkins is an open-source automation server used for building, testing, and deploying code changes. It supports Continuous Integration and Continuous Delivery by automating the software development process.

### Benefits

* Automation - Jenkins automates repetitive tasks, which reduces manual errors and improves efficiency.
* Integration - It integrates with a wide range of tools and plugins, providing flexibility in the development ecosystem.
* Extensibility - Jenkins is highly extensible, allowing users to create custom plugins or integrate existing ones.
* Scalability - With Jenkins, we're able to manage CI/CD for small or large projects.
* Community - Jenkins has a very extensive community, which gives access to extensive documentation and support.

### Disadvantages

* Complexity - Setting up, configuring and maintaining Jenkins can be challenging.
* Security - Keeping Jenkins secure requires constant vigilance. (Why?)
* Resource Consumption - Jenkins may require significant resources, and improper configuration can lead to performance issues.

### Stages of Jenkins

1. Source code management - Fetching the source code from version control.
2. Build - Compile and package the application.
3. Test - Run unit and integration tests to ensure functionality.
4. Deploy - Push the code to various environments (staging, testing, production).
5. Monitor - Monitoring and collecting feedback on the deployed application. During this process we track the performance and stability of the deployment.


![diagram-ci-cd.png](../../readme-images/diagram-ci-cd.png)


### Alternatives to Jenkins

There's a few alternatives to using Jenkins:

* GitHub Actions - Which has built-in CI/CD platform for GitHub repositories.
* CircleCI - It's a cloud-based CI/CD platform with a user-friendly interface.
* Travis CI - Open-source CI/CD platform known for its ease of use.
* TeamCity
* Bamboo

### Why is it referred as a Pipeline?

A CI/CD pipeline is an automated software delivery process that combines the practices of continuous integration (CI) and continuous delivery (CD). It is essentially an assembly line for building, testing, and deploying software updates.

![diagram-ci-cd-pipeline-diagram.png](../../readme-images/diagram-ci-cd-pipeline-diagram.png)

### Why build a Pipeline?

There's several compelling reasons to build a CI/CD pipeline:
* The biggest reason to have CI/CD pipelines is to get the usable software into the hands of the end users. 
* Increased speed and efficiency:
* Improved quality and reliability / Consistency:
* Enhanced collaboration and communication:


## Building a CI / CD pipeline with Jenkins

![jenkins-ci-cd-diagram.png](../../readme-images/jenkins-ci-cd-diagram.png)

### Notes to integrate further

* When a change is made in dev, have they been fully tested yet? There should be a system to of how you test it.
* Main branch is production ready code only.
* Pipeline will take care of testing and mergin into dev.
* 