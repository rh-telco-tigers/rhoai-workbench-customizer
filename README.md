# RHOAI-Workbench-Customizer

The RHOAI-Workbench-Customizer project is designed to update the RHOAI base image with custom Dockerfile snippets, and then publish the updated image to the RHOAI settings image page. This pipeline enables efficient and dynamic updates to the RHOAI workbench without requiring complete Dockerfile rewrites.

## Prerequisites

- Access to an OpenShift cluster
- OpenShift CLI (`oc`) installed

## Getting Started

Follow these steps to set up and run the RHOAI-Workbench-Customizer pipeline:

### 1. Clone the Repository

Start by cloning this repository to your local machine. Use the following command:

```bash
git clone https://github.com/rh-telco-tigers/rhoai-workbench-customizer.git
cd rhoai-workbench-customizer
```

### 2. Create a New OpenShift Project
```
oc new-project cicd-pipeline
```

### 3. Set Permissions
Allow the service account in your newly created `cicd-pipeline` project to create `BuildConfig` and `ImageStream` resources in the `redhat-ods-applications` namespace. You can modify the service account permissions by applying the following role:
```
oc policy add-role-to-user edit system:serviceaccount:cicd-pipeline:pipeline -n redhat-ods-applications
```

### 4. Deploy the Pipeline
Apply `pipeline.yaml` to the `cicd-pipeline` namespace:
```
oc apply -f pipeline.yaml -n cicd-pipeline
```
### 5. Deploy Task

Apply `helm-upgrade-from-source.yaml` and `openshift-client.yaml` to the `cicd-pipeline` namespace.
```
oc apply -f tasks/helm-upgrade-from-source.yaml  -n cicd-pipeline
oc apply -f tasks/openshift-client.yaml  -n cicd-pipeline
```

### 6. Trigger the pipeline from UI.

