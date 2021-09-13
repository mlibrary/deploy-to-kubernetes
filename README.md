# deploy-to-kubernetes
Action for deploying a ghcr image to a kuberenetes cluster

To use this action:
```
   - name: Deploy to NAMESPACE
      uses: mlibrary/deploy-to-kubernetes@v1
      with:
        github_username: ${{ github.actor }}
        github_token: ${{ secrets.GITHUB_TOKEN }}
        image: ORGANIZATION/IMAGE_NAME:TAG
        cluster_ca: YOUR_BASE64_ENCODED_CLUSTER_CA
        cluster_server: YOUR_KUBERNETES_SERVER
        namespace_token: YOUR_BASE64_ENCODED_TOKEN_FOR_DEPLOYING_TO_YOUR_NAMESPACE
        namespace: NAMESPACE_YOUR_ARE_DEPLOYING_TO
        deployment: YOUR_DEPLOYMENT_NAME #default is 'web'
        container: YOUR_CONTAINER_NAME #default is 'web'
```
