# deploy-to-kubernetes
Action for deploying a ghcr image to a kuberenetes cluster

## Example
To use this action to deploy a deployment image:
```
   - name: Deploy to NAMESPACE
      uses: mlibrary/deploy-to-kubernetes@v1
      with:
        image: myorganization/my_app:latest
        github_token: ${{ secrets.GITHUB_TOKEN }}
        cluster_server: my-kubernetes-server
        cluster_ca: ${{ secrets.KUBERNETES_CA }}
        namespace_token: ${{ secrets.NAMESPACE_CA }}
        namespace: my-app-namespace
       
```

To use this action to deploy a cronjob image
```
   - name: Deploy to NAMESPACE
      uses: mlibrary/deploy-to-kubernetes@v1
      with:
        image: myorganization/my_app:latest
        github_token: ${{ secrets.GITHUB_TOKEN }}
        cluster_server: my-kubernetes-server
        cluster_ca: ${{ secrets.KUBERNETES_CA }}
        namespace_token: ${{ secrets.NAMESPACE_CA }}
        namespace: my-app-namespace
        type: cronjob
        cronjob_name: my-cronjob-name
       
```

## Required Arguments

### `image`

The image to deploy. `ghcr.io/` is prepended, so if you provide e.g.
`myorganization/my_app:latest`, the actual image that will be used is
`ghcr.io/myorganization/my_app:latest`.

### `github_token`

The PAT to use to log in to GHCR. This shold be `${{ secrets.GITHUB_TOKEN }}`. 

### `cluster_server`

The Kubernetes server. 

### `cluster_ca`

The Kubernetes cluster CA certificate, base64-encoded, e.g. from:

```bash
cat ~/.kube/certs/my-cluster/k8s-ca.crt | base64
```

### `namespace_token`

A base64-encoded Kubernetes service account token that can be used to set the
image for the given deployment in the given namespace, e.g. from:

```bash
kubectl -n my-namespace get -o json secret my-service-token | jq -r .data.token
```

### `namespace`

The Kubernetes namespace to deploy to. 

## Optional Arguments

These inputs all have defaults.

### `deployment`

The deployment whose image to set. Defaults to `web`.

### `container`

The container in the deployment whose image to set. Defaults to `web`.

### `github_username`

The username to use to log in to GCHR. Defaults to `${{ github.actor }}`. In
most cases you should not need to change this.

### `type`

The options are here are 'deployment' or 'cronjob'. Specfy 'cronjob' if a cronjob's image should be updated. Defaults to 'deployment'

### `cronjob_name`

Only needed if `type` is 'cronjob'. This is the name of the cronjob to which the new image should be applied.
