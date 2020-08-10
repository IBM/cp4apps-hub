# Certified Stack Hub

This document describes the criteria a Devfile application stack must implement to be considered a certified application stack.

## Certification Criteria
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in [BCP
14](https://tools.ietf.org/html/bcp14)
[[RFC2119](https://tools.ietf.org/html/rfc2119)]
[[RFC8174](https://tools.ietf.org/html/rfc8174)] when, and only when, they
appear in all capitals, as shown here.

### Stack structure

* A certified Application Stack MUST also be an [Application Stack](), having the necessary files needed to fulfill core scenarios by the architect (Champ) and the developer (Jane). ** TO DO - Add link to a document that describes an application stack**

* Stacks MUST have a deployment manifest defined in the devfile, using the `alpha.deployment-manifest` property ,that specifies the deployment of its application runtime container, using either:
  * The Runtime Component Operator
  * A runtime-specific Operator with equivalent functionality, such as the Open Liberty Operator

* Stacks MUST contain one or more starter projects, which demonstrate best practices and programming models that a stack user can follow to get started.  

### Capabilities

* Stacks MUST provide mechanisms to execute "inner loop" functions used for developing, debugging and running (non-production) the microservice.  A common way is via a `Dockerfile`, but equivalent mechanisms are also acceptable, as long as they yield a development application container image.  

### Containers

* Stacks MUST have a mechanism to build a container image used for production-grade deployment of the microservice.  This image MUST be free of compilation tools and unnecessary packages (including the source code).  A common way to achieve this is via a `multi-stage Dockerfile`, but equivalent mechanisms are also acceptable, as long as they yield a production application container image.  

* Any container image used in the application stack MUST comply with the following requirements (note: all of the requirements below are automatically checked via Red Hat's Certification scan.  IBMers can visit [this page](https://playbook.cloudpaklab.ibm.com/getting-started/red-hat-openshift/image-certification/red-hat-certification-portal-and-apis).  Non-IBMers can visit [this page](https://connect.redhat.com/resources/container-certification-overview)).  

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
    
### Commercial support

* The base principle is that every CP4A-entitled user (using "Accelerators for Teams" ratio) must be entitled to full commercial support by engaging (only) with IBM for every aspect of a certified stack.
  * "Every aspect" includes but is not limited to:
    * The development and production images (customization code is treated as 3rd party, but supported if within best practices)
    * Any scripts/etc used to create the final dev/runtime image
    * Any runtime or framework or library used by the stack
    
  * "Commercial support" means:
    * customer support (L2)
    * product support (L3)
    * include off-hours for critical situations
        
* Engineers performing the work MUST onboard into the support platform.
   * IBM-internal link to what that entails: https://github.ibm.com/IBMCloudPak4Apps/icpa-support/wiki/L3-onboarding
   * One-of:
     * An entry in https://ibm.biz/WASQueue detailing how L3 can be contacted in a formal support platform (such as the IBM Support Community)
     * An explicit, confirmed agreeement with another support or development organization to take escalations to what we'd call L3 (such as RHR)
   
* Every significant stack release MUST include skills Transfer Education from Development to L2
