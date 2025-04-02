# Generate SBOM Action

This GitHub Action generates a Software Bill of Materials (SBOM) for Python applications using CycloneDX and uploads it to Dependency Track. It helps ensure that your projects have a complete inventory of components and dependencies, which is essential for managing security vulnerabilities.

## Features

- **Python Support**: Specifically designed for Python applications.
- **SBOM Generation**: Uses Syft to generate an SBOM in CycloneDX format.
- **Integration with Dependency Track**: Uploads the SBOM to a Dependency Track server for further analysis.

## Inputs

| Name            | Description                                 | Required | Default       |
|-----------------|---------------------------------------------|----------|---------------|
| python_version   | Python version to setup                    | Yes      | 3.x           |
| server_hostname  | Dependency Track server hostname            | Yes      |               |
| api_key          | API key for Dependency Track                | Yes      |               |
| project_name     | Project name for Dependency Track           | Yes      |               |
| project_version  | Project version for Dependency Track        | Yes      |               |
| bom_filename      | Filename for the BOM                       | No       | ./sbom.json   |

## Usage

To use this action in your workflow, add the following steps to your job:

```yaml
name: Generate SBOM
on:
  push:
    branches: [ "main" ]
  tags: [ 'v*.*.*' ]

jobs:
  build-and-upload:
    runs-on: ubuntu-latest
    steps:
      - name: Generate and Upload SBOM
        uses: USEPA/ccte-sbom-generator-python@main
        with:
          python_version: '3.9'
          server_hostname: 'ccte-api-dependency-track.epa.gov'
          api_key: ${{ secrets.SECRET_OWASP_DT_KEY }}
          project_name: 'Your-Project-Name'
          project_version: ${{ github.ref_name }}
