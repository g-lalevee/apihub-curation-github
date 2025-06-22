# Apigee Api Hub: Curation process using Github files

[![PyPI status](https://img.shields.io/pypi/status/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/) 

**This is not an official Google product.**<BR>This implementation is not an official Google product, nor is it part of an official Google product. Support is available on a best-effort basis via GitHub.

***

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