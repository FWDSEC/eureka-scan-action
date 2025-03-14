# Eureka DevSecOps GitHub Action

The Eureka DevSecOps platform centralizes management of application and cloud security tools, aggregates and correlates the output from security scanners and manual sources into a single pane of glass for easy triage. 

The Eureka DevSecOps GitHub Action seamlessly integrates the Eureka DevSecOps platform into your GitHub workflows, enabling automated security scanning across your repositories. 

By integrating this action, you can run a customized suite of security scans on each repositor to  identify vulnerabilities, and efficiently manage security risks directly from the Eureka Portal.

## Requirements

The Eureka DevSecOps GitHub action is currently only available to existing Eureka DevSecOps users. 

If you are not an existing Eureka DevSecOps user and would like to learn more about Eureka 
DevSecOps to get started, visit the official [Eureka DevSecOps Website](https://www.eurekadevsecops.com/)

## Usage

To use the Eureka DevSecOps GitHub Action, you must generate values for the required secret variables from the Eureka Portal. Once generated, add each secret variable name and its corresponding value to your repository’s GitHub Actions secrets under Settings > Secrets and variables > Actions.

- **EUREKA_ENDPOINT**
- **EUREKA_USER**
- **EUREKA_PASSWORD**
- **PROFILE_INFO**

For more detailed information on required secret variables and generating them from the Eureka Portal, see the [Eureka DevSecOps User Guide]()

### Add Eureka DevSecOps to your existing GitHub workflow:

Copy the following snippet below and add it to the `jobs` section of your GitHub workflow file:

```yml
  eureka-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Run Eureka Scan
        uses: FWDSEC/eureka-scan-action@latest
        env:
          EUREKA_ENDPOINT: ${{ secrets.EUREKA_ENDPOINT }}
          EUREKA_USER: ${{ secrets.EUREKA_USER }}
          EUREKA_PASSWORD: ${{ secrets.EUREKA_PASSWORD }}
          PROFILE_INFO: ${{ secrets.PROFILE_INFO }} 
```

Once added to your desired GitHub workflow, Eureka DevSecOps will start scanning your code with the customized scanner settings and will report discovered vulnerabilities to the configured Eureka system which can be viewed on the Eureka Portal.
