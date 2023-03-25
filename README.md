# moodle-bitnami-charts


https://github.com/rancher/local-path-provisioner
https://github.com/bitnami/charts/tree/main/bitnami/moodle

Install storageclass
```
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.24/deploy/local-path-storage.yaml
```

```
Error: UPGRADE FAILED: execution error at (moodle/templates/NOTES.txt:99:4):
PASSWORDS ERROR: You must provide your current passwords when upgrading the release.
                 Note that even after reinstallation, old credentials may be needed as they may be kept in persistent volume claims.
                 Further information can be obtained at https://docs.bitnami.com/general/how-to/troubleshoot-helm-chart-issues/#credential-errors-while-upgrading-chart-releases

    'moodlePassword' must not be empty, please add '--set moodlePassword=$MOODLE_PASSWORD' to the command. To get the current value:

        export MOODLE_PASSWORD=$(kubectl get secret --namespace "default" my-moodle-release -o jsonpath="{.data.moodle-password}" | base64 -d)

    'mariadb.auth.rootPassword' must not be empty, please add '--set mariadb.auth.rootPassword=$MARIADB_ROOT_PASSWORD' to the command. To get the current value:

        export MARIADB_ROOT_PASSWORD=$(kubectl get secret --namespace "default" my-moodle-release-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 -d)

    'mariadb.auth.password' must not be empty, please add '--set mariadb.auth.password=$MARIADB_PASSWORD' to the command. To get the current value:

        export MARIADB_PASSWORD=$(kubectl get secret --namespace "default" my-moodle-release-mariadb -o jsonpath="{.data.mariadb-password}" | base64 -d)

```

```
export MOODLE_PASSWORD=$(kubectl get secret --kubeconfig /path/to/kubeconfig --namespace "default" my-moodle-release -o jsonpath="{.data.moodle-password}" | base64 -d)

export MARIADB_ROOT_PASSWORD=$(kubectl get secret --kubeconfig /path/to/kubeconfig --namespace "default" my-moodle-release-mariadb -o jsonpath="{.data.mariadb-root-password}" | base64 -d)

export MARIADB_PASSWORD=$(kubectl get secret --kubeconfig /path/to/kubeconfig --namespace "default" my-moodle-release-mariadb -o jsonpath="{.data.mariadb-password}" | base64 -d)

helm --kubeconfig /path/to/kubeconfig upgrade -f ./values.yaml my-moodle-release bitnami-repo/moodle --set moodlePassword=$MOODLE_PASSWORD --set mariadb.auth.rootPassword=$MARIADB_ROOT_PASSWORD --set mariadb.auth.password=$MARIADB_PASSWORD
```