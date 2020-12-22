# Compilation, Deployment & Release

The deployment of the MABS Worker is performed by a pipeline from AWS CodePipeline. You can find instruction here to deploy a new version of:
 - [MABS Adroid Worker Dev](###-mabs-android-worker-:::-deployment-to-the-development-environment)
 - [MABS Adroid Worker QA-PRD](###-mabs-android-worker-:::-release-to-quality-assurance-and-production-environments) 
 - [MABS iOS Worker Dev](###-mabs-ios-worker-:::-deployment-to-the-development-environment)
 - [MABS iOS Worker Qa](###-mabs-ios-worker-:::-release-to-quality-assurance)
 - [MABS iOS Worker Prd](###-mabs-ios-worker-:::-release-to-production).

## Development Environment

### MABS Android Worker ::: Deployment to the Development Environment

To deploy your changes into the Development Stage, you will have to execute the following steps:

1. On the `root` folder of the project run the command `npm run bundle-android --mabs=[7|6|5|3] --revision=x.x.x`. This will generate a `mabs_worker_dev.zip` file. 
    - ##### The `revision` must match a Github revision. This information will be used to tag the Docker image.
2. Access our DevOps AWS Account, go to the S3 service and upload the previously created `mabs_worker_dev.zip` file into the `mabs-codepipeline` bucket.
3. Go to the CodePipeline service, select the `mabs-worker-v2-pipeline-dev` pipeline and wait for its completion.

**Note:** The Source Stage may take a little longer to start running. You can refresh your browser until the pipeline is running.        

### MABS iOS Worker ::: Deployment to the Development Environment

To deploy your changes into the Development Stage, you will have to execute the following steps:

1. On the `root` folder of the project run the command `npm run bundle-ios --mabs=[7|6] --revision=x.x.x --tag=[bootstrap|deploy|halt|start]`. This will generate a `mabs_ios_worker_dev.zip` file. 
2. Access our DevOps AWS Account, go to the S3 service and upload the previously created `mabs_ios_worker_dev.zip` file into the `mabs-codepipeline` bucket.
3. Go to the CodePipeline service, select the `mabs-ios-worker-v2-pipeline-dev` pipeline and wait for its completion.

**Note:** The Source Stage may take a little longer to start running. You can refresh your browser until the pipeline is running.        

## QA and Production Environments 

### MABS Android Worker ::: Release to Quality Assurance and Production Environments

To release a new version of the MABS Android Worker, you will have to execute the following steps:

1. On the `root` folder of the project run the command `npm run release-android --mabs=[7|6|5|3] --revision=x.x.x`. This will generate a `mabs_worker_release.zip` file.
    - ##### The `RepoRevision` must mach a GitHub revision. This information will be used to tag the Docker image.
2. Access our DevOps AWS Account, go to the S3 service and upload the previously created `mabs_worker_release.zip` file into the `mabs-codepipeline` bucket.
3. Go to the CodePipeline service, select the `mabs-worker-v2-pipeline-qa-prd` pipeline and wait for its completion.

The aforementioned pipeline will ensure the deployment of the MABS Android Worker to the QA Environment.
If the deployment to the QA Environment succeeds, the pipeline will be stopped at the stage ApproveForProduction.

To deploy the new version of the MABS Android Worker in the Production Environment, you will have to execute the following steps:
1. Go to the CodePipeline service, select the pipeline `mabs-worker-v2-pipeline-qa-prd`, and wait for its completion.
2. Go to the stage ApproveForProduction and click on the Review button.
3. Enter your comments and Reject or Approve the staging to the Production Environment. 

### MABS iOS Worker ::: Release to Quality Assurance 

To release a new version of the MABS Android Worker, you will have to execute the following steps:

1. On the `root` folder of the project run the command `npm run test-ios --mabs=[7|6] --revision=x.x.x --tag=[bootstrap|deploy|halt|start]`. This will generate a `mabs_ios_worker_qa.zip` file.
2. Access our DevOps AWS Account, go to the S3 service and upload the previously created `mabs_ios_worker_qa.zip` file into the `mabs-codepipeline` bucket.
3. Go to the CodePipeline service, select the `mabs-ios-worker-v2-pipeline-qa` pipeline and wait for its completion.

**Note:** The Source Stage may take a little longer to start running. You can refresh your browser until the pipeline is running.        

### MABS iOS Worker ::: Release to Production 

To deploy the new version of the MABS iOS Worker in the Production Environment, you will have to execute the following steps:

1. On the `root` folder of the project run the command `npm run release-ios --mabs=[7|6] --revision=x.x.x --tag=[bootstrap|deploy|halt|start]`. This will generate a `mabs_ios_worker_release.zip` file.
2. Access our DevOps AWS Account, go to the S3 service and upload the previously created `mabs_ios_worker_release.zip` file into the `mabs-codepipeline` bucket.
3. Go to the CodePipeline service, select the `mabs-ios-worker-v2-pipeline-prd` pipeline and wait for its completion.

**Note:** The Source Stage may take a little longer to start running. You can refresh your browser until the pipeline is running.        
