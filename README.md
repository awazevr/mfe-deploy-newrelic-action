# mfe-deploy-newrelic-action
This is a GitHub Action meant to be used as a [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) within an existing workflow. This action encapsulates the steps necessary to deploy the associated newrelic stack with an Awaze MFE.

## Inputs

### `aws-access-key-id`

**Required** The associated AWS Secret Key Id for a given AWS Account.

### `aws-secret-access-key`

**Required** The associated AWS Secret Access Key for a given AWS Account. 

### `aws-region`

**Required** Specifies the AWS Region to use.

### `app-name`

**Required** The programatic name of your MFE (e.g. search-mfe).

### `deploy-environment`

**Required** The newrelic environment to deploy to (pprd|prd)

### `new-relic-api-key`

**Required** Newrelic API key

### `pagerduty-service-key`

**Required** Pagerduty service key

## Usage
You can use this composite Action in your own workflow by adding:

```yml
name: composite

on:
  push:
    branches: [ main ]

  workflow_dispatch:

env:
  APP_NAME: ${{ github.event.repository.name }}

jobs:
    deploy_pprd:
      environment: pprd
      runs-on: ubuntu-latest

      steps:
        - name: Deploy newrelic pprd
          uses: awazevr/mfe-deploy-newrelic-action@v1.0.0
          with:
            app-name: ${{ env.APP_NAME }}
            deploy-environment: pprd
            aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
            aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
            aws-region: eu-west-2
            new-relic-api-key: ${{ secrets.NEWRELIC_API_KEY }}
            pagerduty-service-key: ${{ secrets.NEW_RELIC_API_KEY }}

    deploy_pprd:
      environment: prd
      runs-on: ubuntu-latest

      steps:
        - name: Deploy newrelic prd
          uses: awazevr/mfe-deploy-newrelic-action@v1.0.0
          with:
            app-name: ${{ env.APP_NAME }}
            deploy-environment: prd
            aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
            aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
            aws-region: eu-west-2
            new-relic-api-key: ${{ secrets.NEWRELIC_API_KEY }}
            pagerduty-service-key: ${{ secrets.NEW_RELIC_API_KEY }}
```

