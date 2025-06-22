# Apigee Api Hub: Curation process using Github files

[![PyPI status](https://img.shields.io/pypi/status/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/) 

**This is not an official Google product.**<BR>This implementation is not an official Google product, nor is it part of an official Google product. Support is available on a best-effort basis via GitHub.


---
## Goal

This repository provides a concrete example of a custom **API Hub Curation** process, built using **Google Application Integration**. This process specifically ingests API metadata from a **GitHub repository**.

API Hub Curation involves transforming and enriching API metadata that has been ingested by Apigee API Hub plugins. For a comprehensive overview, refer to the [Apigee API Hub Curation documentation](https://cloud.google.com/apigee/docs/apihub/curations).

The curation logic implemented here performs the following steps for each ingested API:

* **Checks for API Specification File:** It verifies if an API specification file is available in the GitHub repository.
    * If **not available**, the API is ingested without any additional enrichment.
    * If **available**, it extracts:
        * **API Version Metadata** from the API specification file.
        * **API Metadata** from an API configuration file.
* **API Renaming:** The API's name is standardized by removing any versioning information (if present) to consolidate all versions under a single, consistent name.


## Prerequisites

To implement this sample, you'll need a GCP account with both Apigee API Hub and Application Integration activated. If needed refer to Google Documentation [Provision API hub](https://cloud.google.com/apigee/docs/apihub/provision)and [Set up Application Integration](https://cloud.google.com/application-integration/docs/setup-application-integration).

You'll also need a GitHub account with privileges that allow setting up external access to your repositories, during Github Integraition Connector setup.


## Github setup

To begin, you'll need a **GitHub repository** to store your configuration and API specification files. If you haven't already, here are some essential GitHub tasks you'll need to complete, depending on your setup:

* **Create a GitHub account**: If you're new to GitHub, start by [creating an account](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github).
* **Create new repositories**: You'll need to [create a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) to host your files.
* **Create a GitHub App** to authenticate connexion from Integration Connexion. See Github documentation [create a GitHub App](https://docs.github.com/en/apps/creating-github-apps/about-creating-github-apps/about-creating-github-apps). 

> ℹ️ One Github App. can allow access to one or many repositories : you can configure it in Github App. permissions.

> ℹ️ the **Client ID** and **Client Secret** generated during this process are crucial for setting up your GitHub Integration Connection. You'll also need the **Callback URL** from your Integration Connection to finalize the GitHub App creation. For more details, refer to the [GitHub Integration Connection documentation](https://cloud.google.com/integration-connectors/docs/connectors/github/configure#configure-the-connector).

## Integration Connexion Setup

Application Integration leverages a **GitHub Integration Connection** to retrieve files from your GitHub repository. Therefore, your initial step is to create this connection by following the instructions provided in the [Configure the GitHub connector documentation](https://cloud.google.com/integration-connectors/docs/connectors/github/configure). Please also refer to the preceding note regarding GitHub App parameters (credentials and call back URL).

## Application Integration Setup

To upload, do the following steps:

1) Clone the repo 
```sh
https://github.com/g-lalevee/apihub-curation-github.git
```
2) In the Google Cloud console, go to the [Application Integration](https://console.cloud.google.com/integrations) page
4) In the navigation menu, click Integrations. The Integrations List page appears.
5) Select an existing integration or create a new integration by clicking Create integration.
If you are creating a new integration:
    - Enter a name `apiHubCurationGithub-v1` and description in the Create Integration dialog.
    - Select a Region for the integration from the list of supported regions.
    - Click Create.
    
    This opens the integration in the integration designer.
6) In the integration designer, click `Upload/download menu` and then select `Upload integration`.
7) In the file browser dialog, select `apiHubCurationGithub-v1.json`, and then click Open. A new version of the integration is created using the uploaded file.
8) In the variable panel, update default values for config variables
    - `CONFIG_githubConnectionName`: the name of the Integration Connection created during step **Application Integration Setup**.
    - `CONFIG_githubRepoName`: the name of the Github repository used to store API specification files and configuration files.
    - `CONFIG_githubRepoOwnerName`: the name of the Github owner name of the repository.
9) In the integration designer, click Deploy.
10) Click Test integration. This runs the integration and displays the execution result in the Test Integration dialog.
