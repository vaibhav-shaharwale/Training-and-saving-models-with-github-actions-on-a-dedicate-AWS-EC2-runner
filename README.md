# Training-and-saving-models-with-github-actions-on-a-dedicate-AWS-EC2-runner

In the project, Continuous Machine Learning (CML) is utilized to automatically retrain models whenever there are changes in the data, model code, or parameters. A pipeline is created to provision an AWS EC2 instance to retrain a model and save the output regularly. This approach helps prevent drift by ensuring that the model always utilizes the latest input data

## CML workflow:
1. Provisioning an Amazon Web Services (AWS) EC2 instance.
2. Training the model.
3. Saving the model and its metrics to a GitHub repository.
4. Creating a pull request with the new outputs.
5. Terminating the AWS EC2 instance.

## Prerequisites
1. AWS Account
2. Github Personal Access Token with repo scope
3. AWS Access_key_id and secret_access_key
4. Add Github personal access token, AWS access_key_id and AWS secret_access_key as github secrets

## Workflows
train.py is a code to train the model and save it as a file, the subsequent step involves setting up a CI/CD pipeline to provision a runner and execute the code. The workflow is defined in a _flow.yaml_ file in the _.github/workflows_. This configuration allows GitHub to automatically execute the workflow upon triggers(on: push).
Every time changes is push to github the workflow get trigger and runner start training and saving the model.

## CML
CML help in exporting of the model from the runner to the Git repository. To enhance the training stage of the workflow, the process involves extending it by _model.joblib_ to a new experiment branch and creating a pull request.

Using the _cml pr_ command specifies the files to include in the pull request. Subsequent commands are employed to generate a report within the pull request, showcasing the confusion matrix and calculated metrics.


#### In various situations, it's beneficial to regularly retrain models. For instance, using the newest data helps to prevent model drift. CML simplifies automating this task.

#### In this project, the focus was on configuring CML for a automating training task using a self-hosted runner. The automation involved setting up this runner on AWS(EC2) and exporting the resulting files to the Git repository. Finally, the runner was terminated to avoid unnecessary charges on AWS
