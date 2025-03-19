# Eureka DevSecOps GitHub Action

The Eureka DevSecOps platform centralizes management of application and cloud security tools, aggregates and correlates the output from security scanners and manual sources into a single pane of glass for easy triage. 

The Eureka DevSecOps GitHub Action seamlessly integrates the Eureka DevSecOps platform into your GitHub workflows, enabling automated security scanning across your repositories.

By integrating this GitHub Action, you can run a customized suite of security scans on each repository to identify vulnerabilities, and efficiently manage security risks directly from the Eureka Portal.

## Requirements

The Eureka DevSecOps GitHub Action is currently only available to existing Eureka DevSecOps users.

If you are not an existing Eureka DevSecOps user and would like to learn more about Eureka 
DevSecOps to get started, visit the official [Eureka DevSecOps website](https://www.eurekadevsecops.com/).

## Usage

To use the Eureka DevSecOps GitHub Action, you must generate values for the required secrets and repository variables from the Eureka Portal listed below. Once generated, add each secret and repository variable name and its corresponding value to your repository’s GitHub Actions secrets under *Settings* > *Secrets and variables* > *Actions*.

Secret Variables:

- **EUREKA_ENDPOINT**
- **EUREKA_USER**
- **EUREKA_PASSWORD**

Repository Variables:

- **PROFILE_INFO**

For more detailed information on required secret variables and generating them from the Eureka Portal, see the [Eureka DevSecOps User Guide](https://eurekadocs.netlify.app/).

## Adding the Eureka DevSecOps Github Action to your GitHub workflow

To integrate the Eureka DevSecOps Github Action into your GitHub workflow, add the following YAML code to the `jobs` section of your existing workflow file:

```yml
  eureka-scan:
    runs-on: ubuntu-latest
    steps:
   - name: Checkout GitHub Action
     uses: actions/checkout@v4
  
      - name: Run Eureka Scan
        uses: FWDSEC/eureka-scan-action@main
        env:
          EUREKA_ENDPOINT: ${{ secrets.EUREKA_ENDPOINT }}
          EUREKA_USER: ${{ secrets.EUREKA_USER }}
          EUREKA_PASSWORD: ${{ secrets.EUREKA_PASSWORD }}
          PROFILE_INFO: ${{ vars.PROFILE_INFO }} 
```

### Enabling Pull Request Scan Reports (Optional)

To generate a Eureka scan report as a comment on an associated pull request, include the `enable_pr_scan_report` input parameter set to `true`:

```yml
eureka-scan:
  runs-on: ubuntu-latest
  steps:
    - name: Checkout GitHub Action
      uses: actions/checkout@v4
        
    - name: Run Eureka Scan
      uses: FWDSEC/eureka-scan-action@main
      env:
        EUREKA_ENDPOINT: ${{ secrets.EUREKA_ENDPOINT }}
        EUREKA_USER: ${{ secrets.EUREKA_USER }}
        EUREKA_PASSWORD: ${{ secrets.EUREKA_PASSWORD }}
        PROFILE_INFO: ${{ vars.PROFILE_INFO }}
      with:
        enable_pr_scan-report: true 
```

- `enable_pr_scan_report: true` enables the Eureka scan report as a comment on the pull request.

### Example: Full Github Workflow with Eureka DevSecOps GitHub Action

If you're creating a new GitHub workflow, you can use the following complete example:

```yml
name: Full GitHub Workflow with Eureka DevSecOps Scan Action

on:
  push:
    branches:
      - "*"

jobs:
  eureka-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout GitHub Action
        uses: actions/checkout@v3

      - name: Run Eureka Scan
        uses: FWDSEC/eureka-scan-action@main
        env:
          EUREKA_ENDPOINT: ${{ secrets.EUREKA_ENDPOINT }}
          EUREKA_USER: ${{ secrets.EUREKA_USER }}
          EUREKA_PASSWORD: ${{ secrets.EUREKA_PASSWORD }}
          PROFILE_INFO: ${{ vars.PROFILE_INFO }}
```

Once you've added or updated your GitHub workflow, commit the changes to your repository.

Eureka DevSecOps can now scan your code using the configured scanners and settings from the Eureka system. Detected vulnerabilities will be reported to the Eureka system and can be viewed on the Eureka Portal.  

> Some scanners may require additional workflow steps for successful scanning. Consult the official [Eureka DevSecOps User Guide](https://eurekadocs.netlify.app/) for more detailed information.
