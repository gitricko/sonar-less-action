[![Test](https://github.com/gitricko/sonarless/actions/workflows/test.yml/badge.svg)](https://github.com/gitricko/sonarless/actions/workflows/test.yml)

# Sonarless v0

This action and its developer friendly helper scripts enable sonarqube scanning for your repository without a need of a dedicated hosted sonarqube server. It boots up a sonarqube docker instance and enable developers to scan checkout code and give a metric json so that you can check the quality of the code.

# Usage

<!-- start usage -->
```yaml
- uses: gitricko/sonarless@v0
  with:
    # Folder path to scan from git-root
    # Default: . 
    sonar-source-path: ''

    # Path to SonarQube metrics json from git-root
    # Default: ./sonar-metrics.json 
    sonar-metrics-path: ''

    # SonarQube Project Name
    # Default: ${{ github.event.repository.name }}
    sonar-project-name: ''

    # SonarQube Project Key
    # Default: ${{ github.event.repository.name }}
    sonar-project-key: ''
```
<!-- end usage -->

# Scenarios

- [Scan all files from git root directory](#Sonar-scan-all-files-from-git-root-directory)
- [Scan particular folder from git root directory](#Scan-particular-folder-from-git-root-directory)
- [Scan code and fail build if metrics below expectation](Scan-code-and-fail-build-if-metrics below-expectation)

## Sonar scan all files from git root directory

```yaml
jobs:
  Sonarless-Scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Sonarless Scan
        uses: gitricko/sonarless@v0
```

## Scan particular folder from git root directory

```yaml
jobs:
  Sonarless-Scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Sonarless Scan
        uses: gitricko/sonarless@v0
        with:
          sonar-source-path: 'src'
```

## Scan code and fail build if metrics below expectation

```yaml
jobs:
  Sonarless-Scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Sonarless Scan
        uses: gitricko/sonarless@v0
        with:
          sonar-source-path: 'src'
          sonar-metrics-path: 'sonar-mymetrics.json'

      - name: Check Sonar Metrics
        uses: gitricko/sonarless@v0
        with:
          sonar-source-path: 'src'
          sonar-metrics-path: 'sonar-mymetrics.json' 
```

# Coffee

If you find this small helper script and action helpful, buy me a [sip of coffee](https://ko-fi.com/gitricko) here to show your appreciation (only if you want to)