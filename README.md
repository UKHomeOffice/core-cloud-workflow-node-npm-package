# Core Cloud Workflow Node npm publish

A GitHub Actions workflow for running npm publish on Node.js projects to identify and report code quality issues.

## Overview

This workflow automates code publishing of Node.js projects within the core-cloud ecosystem, ensuring code quality standards are met.

## Features

- Automated npm publish
- Using node access token to access npm or github

## Requirements

- Valid `package.json`, `package-lock.json`
- Valid registry to publish to

## Usage

Reference this workflow in your GitHub Actions pipeline:

```yaml
jobs:
    publish:
        uses: UKHomeOffice/core-cloud-workflow-node-npm-publish
        with:
            node_access_token: ${{ secrets.NPM_TOKEN }}

```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `working_directory` | Directory to run npm publish in | No | `.` |
| `node_version` | Node version | No | `24` |
| `access_level` | The access level for the npm package (e.g., public or restricted)| No | `public` |
| `node_access_token` | The npm access token to authenticate publishing | Yes | `` |


## Outputs

| Output | Description |
|--------|-------------|
| `npm_publish_exit_code` | Exit code from npm publish (0 = success) |

## Support

For issues or questions:
- Create an issue in this repository
- Contact the Sauron Team on Slack: #core-cloud-team-sauron
- For tag enforcement questions, contact the Checkov workflow maintainers: #core-cloud-team-sauron

---

## Updated Repository Structure
```
core-cloud-workflow-node-npm-publish/
.github
├── workflows
|    └── self-test.yaml // TODO 
|
├── action.yaml
├── CODEOWNERS
├── README.md
└── tests
    ├── test-publish-invalid/
    └── test-publish-valid/
```

### 📘 SonarQube Configuration 
– `sonar-project.properties`

```
sonar.exclusions=tests/**

```

This removes all test fixtures and example IaC from SonarQube analysis, ensuring the Quality Gate only evaluates the actual workflow, action code, and scripts.

| Directory           | Purpose                                               | Excluded From SAST? |
| ------------------- | ----------------------------------------------------- | ------------------- |
| `tests/**`          | Local npm publish test harness (intentionally invalid code) | ✅ Yes               |
| `action.yaml`       | Composite action logic                                | ❌ No                |

This setup ensures clean SAST results without blocking PRs due to intentionally invalid IaC.

## Contributing

Please read [CONTRIBUTING.md](./CONTRIBUTING.md)

## Security

Please read [SECURITY.md](./SECURITY.md)