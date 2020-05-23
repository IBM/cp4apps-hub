# Certified Stack Hub

This repository hosts a certified Application Stacks Hub referencing Application Stacks that have met the certification criteria outlined below. 

## Certification Criteria
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in [BCP
14](https://tools.ietf.org/html/bcp14)
[[RFC2119](https://tools.ietf.org/html/rfc2119)]
[[RFC8174](https://tools.ietf.org/html/rfc8174)] when, and only when, they
appear in all capitals, as shown here.

* A certified Application Stack MUST also be an [Application Stack](https://appsody.dev/docs/stacks/stacks-overview), having the necessary files needed to fulfill core scenarios by the architect (Champ) and the developer (Jane).  Today that is based on `Appsody`, tomorrow will be based on `devFile` (odo). 

* Stacks SHOULD contain a `stack.yaml` with [custom stack variables](https://appsody.dev/docs/stacks/develop/#custom-stack-variables) to update key versions of the source code if applicable (e.g. POM files) and runtime container image (e.g. Dockerfiles could have `FROM {{.stack.base-deploy-image}}`).

* Stacks MUST have a `app-deploy.yaml` file that specifies the deployment of its application runtime container, using either:
  * The Runtime Component Operator
  * A runtime-specific Operator with equivalent functionality, such as the Open Liberty Operator

* Stacks MUST have a mechanism to build a container image used for developing, debugging and running (non-production) the microservice.  A common way is via a `Dockerfile`, but equivalent mechanisms are also acceptable, as long as they yield a development application container image.

* Stacks MUST have a mechanism to build a container image used for production-grade deployment of the microservice.  This image MUST be free of compilation tools and unnecessary packages (including the source code).  A common way to achieve this is via a `multi-stage Dockerfile`, but equivalent mechanisms are also acceptable, as long as they yield a production application container image.  

* Stacks MUST contain one or more code templates, which demonstrate best practices and programming models that a stack user can follow to get started.

* The Stacks' development application container image as well as its production application container image MUST comply with the following requirements (note: all of the requirements below are automatically checked via Red Hat's Certification scan.  IBMers can visit [this page](https://playbook.cloudpaklab.ibm.com/getting-started/red-hat-openshift/image-certification/red-hat-certification-portal-and-apis).  Non-IBMers can visit [this page](https://connect.redhat.com/resources/container-certification-overview)).
  * MUST use an Universal Base Image (UBI) or Red Hat Enterprise Linux (RHEL) as the base Operating System of the image and only include RPM packages from the UBI / RHEL repositories.
  
  * MUST use a [Red Hat Runtimes](https://www.redhat.com/en/products/runtimes) base runtime container image if applicable.  For example, using the Spring Boot base runtime container from Red Hat Runtimes instead of a community Spring Boot base runtime container.
  
  * SHOULD use a base runtime container image that comes from the [Red Hat Registry](https://catalog.redhat.com/software/containers/explore) if available.  For example, if there's an image available from both Docker Hub and Red Hat Registry, the stack should reference the version from the Red Hat Registry.
  
  * SHOULD NOT modify the underlying Operating System from base runtime container image (e.g. `yum updates`) but may add specific packages that are required.
  
  * MUST include the following labels:
    * name: Name of the image
    * vendor: Company name
    * version: Version of the image
    * release: A number used to identify the specific build for this image
    * summary: A short overview of the application or component in this image
    * description:  A long description of the application or component in this image

  * MUST NOT contain any critical or important vulnerabilities, as defined at https://access.redhat.com/security/updates/classification.
  
  * SHOULD have less than 40 layers when uncompressed.

  * SHOULD always be tagged with a version other than `latest`.
  
  * MUST include software terms and conditions.
    * Create a directory named /licenses and include all relevant licensing and/or terms and conditions as text file(s) in that directory.
   
  * MUST not run as the root-user by default and MUST be able to run as a randomly chosen UID with GID of 0 (root).  More information can be seen under `SUPPORT ARBITRARY USER IDS` in [this article](https://docs.openshift.com/container-platform/4.3/openshift_images/create-images.html#images-create-guide-openshift_create-images).
  
  * MUST not request host-level privileges.
    
  * SHOULD support multiple architectures, such as x86, ppc64le and s390x, via a manifest list. For more information see [the manifest tool](https://github.com/estesp/manifest-tool/releases).
    
    
