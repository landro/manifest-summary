# manifest-summary

Read a Kubernetes manifest and print a table of its contents.

## Installation

```
$ go install github.com/landro/manifest-summary
```

Requires Go to install.

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
