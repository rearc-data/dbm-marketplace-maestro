# Databricks Marketplace Notebook Auto-Generation

This notebook is used to generate and deploy notebooks in bulk to the Databricks Marketplace. The notebook takes the following steps:
1. Retrieves the API URL, token, user, and workspace ID associated with the notebook's context, if they exist.
2. Retrieves the API URL, API token, and notebook path from the notebook's context JSON.
3. Retrieves a list of all Marketplace listings associated with the Databricks account.
4. For each Marketplace listing, finds the number of tables in the share and adds this number to the listing metadata to determine what type of Pandas Profiling to use.
5. Provides four kinds of notebooks to generate, depending on how many tables are in the share, how large they are, etc.:
    - Pandas Profiling [Full]
    - Pandas Profiling [Minimal]
    - Time-Series
    - Simple
6. Generates and runs a new Databricks ntoebook based on teh specificied Marketplace listing and notebook type.
7. Uploads a notebook to a Databiricks marketplace

## Setup

To run this, you will need to enter the following Databricks account sepecific information manually:
- Databricks account hash
- Databricks provider name
- Provider contact email
- Provider terms-of-service link
- Provider privacy policy link

## Options
This template provides four kinds of notebooks that can be generated, depending on how many tables are in the share, how large they are, etc.
- **Pandas Profiling [Full]** 
   - Applies full Pandas Profiling. 
   - Good for most shares.
- **Pandas Profiling [Minimal]** 
    - Applies a smaller version of Pandas Profiling. 
    - Good for shares with many tables, or large datasets with many columns/rows.
- **Time-Series** 
    - Gives a time-series plot for each numeric column, along with a scatter-matrix in some cases. 
    - Great for time-series datasets.
- **Simple** 
    - Only provides sample data and summary statistics for each table. 
    - Good for shares with very many tables.

## Deployment
To deploy a notebook to a Marketplace listing, simply run the **_create_notebook_for_listing_** function for each desired listing with the appropriate arguments:
- __listing__: A JSON object representing a Marketplace listing.
- __notebook_type__: A string indicating the type of notebook to generate. Supported values are:
    - 'Pandas Profiling [Full]'
    - 'Pandas Profiling [Minimal]'
    - 'Time-Series'
    - 'Simple'
- __handle_existing_notebook__: what to do if the listing already has a notebook attached to it:
    - 'replace': replace the existing notebook with the new one (default)
    - 'skip': skip the upload and do nothing
    - 'append': add as a second notebook
