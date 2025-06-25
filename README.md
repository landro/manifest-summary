# manifest-summary

Read a Kubernetes manifest and print a table of its contents.

## Installation

### 1. Install Golang

- **macOS (Homebrew):**
  ```bash
  brew install golang
- **Linux / Windows:**
    Follow the official [Go installation guide](https://golang.org/doc/install)

### 2. Install manifest-summary:
```bash
 go install github.com/landro/manifest-summary@latest
```
This installs the binary to your Go bin directory.
### 3. Export Go bin to your $PATH
```
export PATH="$PATH:$(go env GOPATH)/bin"
```

## Usage

Pipe your Kubernetes configuration into the `manifest-summary` binary.

```
$ curl -s https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/wordpress/mysql-deployment.yaml | manifest-summary
+-------------+-----------------------+-----------+-----------------+
| API VERSION |         KIND          | NAMESPACE |      NAME       |
+-------------+-----------------------+-----------+-----------------+
| v1          | Service               |           | wordpress-mysql |
| v1          | PersistentVolumeClaim |           | mysql-pv-claim  |
| apps/v1     | Deployment            |           | wordpress-mysql |
+-------------+-----------------------+-----------+-----------------+

$ curl -s https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/demo/basic/sync.yaml | manifest-summary
+-------------------------------+--------+-------------------+--------+
|          API VERSION          |  KIND  |     NAMESPACE     |  NAME  |
+-------------------------------+--------+-------------------+--------+
| config.gatekeeper.sh/v1alpha1 | Config | gatekeeper-system | config |
+-------------------------------+--------+-------------------+--------+
```

## Helm Chart Example
Use manifest-summary to inspect rendered Helm charts before applying them.

### 1. Add a Helm chart repository
Example using DataHub:

```bash
helm repo add datahub https://helm.datahubproject.io/
helm repo update
```

### 2. Render and summarize the manifest:

```bash
helm template my-release datahub/datahub-prerequisites \\
  --values values.yaml | manifest-summary
```
This prints a summary of the Kubernetes resources that will be created.


