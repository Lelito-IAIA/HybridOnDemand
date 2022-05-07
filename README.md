# HybridOnDemand (onCloudPart)
## On Linode
Create 3 new cluster on Linode with v. 1.21 of kubernates (LONDON).
The first cluster will work as Management cluster. It will manage all the incoming traffic and will decide where send all the incoming request.
The second and the third clusters will work as production cluster and they will be the place where we will deploy all the stuff.

Create a new kubeconfig.yaml file and add the info about every cluster stored in the kubeconfig file of each cluster.
(clusuter, user name, context):
``` 
apiVersion: v1
kind: Config
preferences: {}

clusters:
#cluster info about mgmt-cluster
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM1ekNDQWMrZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJeU1ERXhNREE1TlRjME5Wb1hEVE15TURFd09EQTVOVGMwTlZvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBUG5HCjV2ajJJZDUzVTF3VHVsNGdmZ0RsZ3JqaGZyOElvSWQ3cGJqRW9FN1RmbHNNVE1FSUc0UVJOeGR3RUMwblVMU2oKbjVPcUR2cDJoSi9STHI4eEI2V0FHYktkSk1KM0hRdWNGay9FdGJIeWJQS0c0cjBJbnpQMzBrWExRM0wvK1R1egpSeGpZdWpCTFBGb0JIWlBHUk5iOXdSVEpLSjNHdjJ1M2R0UHhwSHBWRUh0QzgvRG5sQWU0VE5oYWsySm9WeDF0CmlCcnNSclp5VG5hcjd5aVlFaVQ0SkttdWxLaTRLczRKZVk0U01XK0VxNjYwUEx3MzBkalAwZVNxb3d3eG5Kc2IKRXoyS3RtcDd5T29ES3Y3V2xsUjJZbFdFSFdWZ3JJdk4wV09Id3RPbU1LQXk0TkZ6U20zNGRFQlU4NlA2aVUvQwpEZ3hIR3ZJWXYzOW1pTFJkcmtFQ0F3RUFBYU5DTUVBd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0hRWURWUjBPQkJZRUZIS2xoaGlPdEZSLzcxR2drRm1LR1RDQ0M2ZDVNQTBHQ1NxR1NJYjMKRFFFQkN3VUFBNElCQVFCd093ZnhkOWRha0hLelMvWi9FMHhlSEhvNHl5NlhjTkdKYW1oUDIrNXdrbk8raFV0NQppT2hrZTFUdCtsMVhOQmZPOEhUM2hDaC9lMUxFOXFDRkxuMVdWRlFBMnNTcTVSbHpmYTdEcjdwd1oxSW9yMXROCnYvZVhZOHdGdkY0MU5Qa1dmRiswMTFOLzhldC8ydE5RMnJWSjh5SkxWemdWSmZTYkMvZi9JOWU5QWNkeUVXTCsKYlpRb28zRjBvekRhMHlTM0tTTFBRNFcrdGRIR1U1WVZlZmlJdU5kaW1OR1B0enNINzdPZk1qMEd2S0xNRTdzNgpHTDU2YXlOT2JuS1k5UU1DQkVrQ2hMdjJJRmNsSnZNUTA2WUltNkdhZzlKWkwydEhDRlRJY1EyR1kxT216NFFUCnZXbVBtNUtYbjZHNWJGREV4Q3RMRktCSUI1dlc4Ni9wNitJQgotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    server: https://ce9784ae-d6d5-437c-8bb1-c60e5a49c5a5.eu-west-2.linodelke.net:443
  name: lke49033
#cluster info about cluster-1
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM1ekNDQWMrZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJeU1ERXhNREE1TlRneU1Wb1hEVE15TURFd09EQTVOVGd5TVZvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBT2ZmCkJrTlE1aEZVc0VNR1ZUcGI2Z1N4bGtzUFBhQ29FcXJlVVFMN084S29BMEtoQy9RYlN3R1lKN0hmYnMxamE5QlkKdWJwaU1QVk91SnNaYVhFS0p1NElxK0h3dTZyVTNVbk5JZFcwUHdJT2pWdU8yNmZTVnNwcEVlNVNNck9lZ29iZQpUNGlPWmJwUkRZVzVyZHh2aXVvWllCRmQyMGZsOTNWK0VSVklHS1puYnIxQXJkdnA5VTlSckRpZloyTHJsM3pFCjF4em4rRkxLUDNiT3V3K3VMZ0g2bkFmazBIWFNGZFpIbU56WGdNQ1dUSEI1KytGQWNPbnV0bnpTTFBIWG96Tk8KeDkxczNGWjJLMEFUdlgrUTBtdGJHbnlUVFcxcDdaR1ltOUFaaTQ4K1dmS1BXclFFRjVQbUJYSTh6Y29ZQXhregpUU1dIbm5mYmdRSVMvSE04ZlY4Q0F3RUFBYU5DTUVBd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0hRWURWUjBPQkJZRUZITVNDNGk3UnY2bjhaTk5ERExxWFEzS3QvbkpNQTBHQ1NxR1NJYjMKRFFFQkN3VUFBNElCQVFEblFlYU1XWnpDTTFGWnQxa2NWeXUrSlVXVHpZS1gvNjR2NUx0a25KZ05tZzRnTVVVbAp0RVhzeFVJaUJuZWY5cjhFUWF6MWVVNTB3NmErc0lMZ3A4MGozY0JqYUlRT2FYUE5tMGptSzdXcGFYbVhuY1RLClQ5ZFBoS0FqQVltbzVHZHVtanhyc0swUGkwT2FudzNNWXd2dnM4SW1EZjI4bHZlcUZ4aEcvb05SM2pJL1FVK0EKd1gxY0I0eENsSjA4RXRhME04c0lJV1RoWTFMRXVtUm94VGlqdElLcEFNL0psZUt0RlhXWC9KR1NYY0lhN1V4dwpUWWUwOW1KVXB4S2dDckhZVHJlZjZHbVkxaU1FME9sMSs4THZIdk1MbjZqY1V1b0UzeVBhM0NqZnRaSW0yVndFCnlLQkNVR0dZQnZlck5NcStQWjh5TVV1NFpyYW1TNnRwZnlSdQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    server: https://bd7a399a-a1c1-4ff1-802a-9a3aacabd6c3.eu-west-1.linodelke.net:443
  name: lke49034
#cluster info about cluster-2
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUM1ekNDQWMrZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJeU1ERXhNREE1TlRnMU1Gb1hEVE15TURFd09EQTVOVGcxTUZvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTHl5Ck9xeS9tdzFxTit1bDRrM3Q4VEkzeVZKYWR5b3NJUlRIZUVlQ080dGlRcUZEK2VwZnoreVlkTXBQa0x2M1lmM3cKTDRiTDh3OU5ZSEZHK3JiNVBBS3hkZjBMUkEyTVFlUS83a3ZhVWY2ODJoeTJHQWpGWDFuanpobDMrRlJiRTIzYQp2RFE4MDhVVXp2MGkzd3RWWHJTYWZoajNsQ1Q4eXRxTG9wd1ZrT1IzUmhlVXRLNytnZGo3RWxpMk5mVWNFTkQ0CjBmeDJlTzQ3eng5aVlQU0l5M3JMKzArZUpuTGxPZmpJYnlFTGR2anNleXMrTlNsNW5FU1F1bHhkZlFOYWNQNTQKOE1VcjF4TnM3dURLaGEzSm1rem1SaHpSd2tkZzdXREhLMmptSHFDc0o3dSt4VkxLTWt6WVBNYUN5YXJIYnFKWApkVXlpVTlHL1M3MXlIbFFjcHA4Q0F3RUFBYU5DTUVBd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0hRWURWUjBPQkJZRUZJWjJrSElYSkZ0UzNObGoxVEpEcXBGWTFJd2NNQTBHQ1NxR1NJYjMKRFFFQkN3VUFBNElCQVFDWXdOTU93WWlYZkdmRnJORm11UEVlc05GSHViTVZSVy8vSmF4QkpLQStTVmo4MTd6NApVdXZBUjN6aFd4QnlsSGJFd3VvZEIzbDdLUXJHRC93L1l1VmtoT1Jpc1RJcDYvbTZuaTR5bUErQjJKRmRJV0M4CjdwZUk3Yms4U0VtUEN4QzQ4TWo0UGgzWFVjQzVtYXhEZ3dvWXBmSWQ0TGx2emJhUndPK05sRWFhaE9kZDBMbmYKUHRaWTB3YWh0NXNzNnl1NWkybEx2UTFyc2dncFVsRnVFMXN6MExKcnh0c0ZqL2Q0aGhQZnZ2S0lSdWFLVXFUTgpLUWR6eVVyalB2a2RtSlUzWFdLYXJBclkraXl4Zkt2RjBkTHZxTDhCUFFEYzdBdC9oUGszU2c0UDBBbGZkWURICjhoNjFuUEx5LzBsUUFhS0k1WktldUxqeUZrL2x5QjU5d0pwdwotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    server: https://6fac2c54-8ae1-449b-9590-daed3fa60dcf.eu-west-2.linodelke.net:443
  name: lke49035
users:
#user info about mgmt-cluster
- name: lke49033-admin
  user:
    as-user-extra: {}
    token: eyJhbGciOiJSUzI1NiIsImtpZCI6IkVpMFZ5bVVUeVpqejAtTnFXUF8wMWg4aElUS2hrZ190dktJVTdKU1JfODAifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJsa2UtYWRtaW4tdG9rZW4tZGRmc2oiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoibGtlLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiNDNlNmU0MWMtNDNjYS00NzM0LThhMTktZDNmMDM1MWJlZjdkIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmUtc3lzdGVtOmxrZS1hZG1pbiJ9.vnZbH5OSnF2dOdfE1Uc-SiAUfbGP9Lvau2DXgJI9I4w2TUV_DxtxcU0aVSiT7HSKumOzUA_JKb3AKzhl0mYxnn6d9VkL-muBmSpckv1yxDjhqT-zlbBjQN6q6mrRan2pNAJ-1DAAIkygm_ifQQIycvgGmhbXB10pGApu1W77wF10kYPMFLzHAkkqy7HSzF7Hp4esGmwYi0VFskvaL5SdyEC7xyCMGicKLOaDlM25bjVAHmBtByp6j5G3bQTVz7ysGucFb_o00VbnWecExfgsI_vIZlSj0eMB6O1Cr68KS1EXclYZNEzXoRi0mXvwZVxURwfOUSHHvTM7l3UGKyX3_g
#user info about cluster-1
- name: lke49034-admin
  user:
    as-user-extra: {}
    token: eyJhbGciOiJSUzI1NiIsImtpZCI6ImtxWl95azB3aXB3X1pOZzBrMkR4bHpPN2dHTWdxWll4dVVCdTg3N3FvNjAifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJsa2UtYWRtaW4tdG9rZW4tZ3dmNHEiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoibGtlLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiMDNjMGRhODEtNjQyOC00OTNhLTlmM2UtYTA1NjZlMTlkNzkzIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmUtc3lzdGVtOmxrZS1hZG1pbiJ9.b_hL60UG4Y6XvWfwVa2Ybus4ZgMuEeG-Lht0PqWYfHOXxOfjVWfpnJCLir5hr_W6KjC4xiAi_eaTt7iWjK_a28g7qRUiH67DvB-bdtmLsJ4RhBxWQ897csWLTG69uDR_vnR7xrQyLYCbUoWkVWrs4jFzmGjO9A4Ko1RYDR_rL2ERb-alTpTxR6j8of1Ml0qabJsvmKlwkzNdUUkNOT72bLzvdM6c4OQICCumbKaflByzdJ2HbjiaJ5DYuDpSAgSjNzFxYj6hHttqlXpnTPfYCjW12YKR1n8tqffHaHTC-Wj5gZKoIHWvWZVKVyr2cU0EW0FkL4w-r-0gFoyB-LLtBQ
#user info about cluster-2
- name: lke49035-admin
  user:
    as-user-extra: {}
    token: eyJhbGciOiJSUzI1NiIsImtpZCI6ImtLQXh3M1lHcmh3WXl4OUd4dFJNVHp2VjdrZVhaT1NINkcxWjZobHdJZGMifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJsa2UtYWRtaW4tdG9rZW4tZ3dienMiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoibGtlLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiOTFiNWIxOTktMzgzNC00MzNiLTk1MzgtMzMxMmE4Y2FjZWNkIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmUtc3lzdGVtOmxrZS1hZG1pbiJ9.y3mI0E8br_O3X2jlrj-K9HOsGCTk8DXGy3HZDOiUyp1zz--6Gcp1E_l2twgetTbZBw_Vt2mQbQKv8s53W8CUSjof_9jJlQFQeMqgO35xlGxy_vKooJtqOWrPkapNGtAuUZhUKjSwmfP3g2u9Uk84EMFW3EqHWGEQ_bMtWggJJGovURK9_MOgeGbmwETVEUHi3lkTM0Fq2Cpfzn_ml40Q_HOgYVm_rTLG195bYMI84RQcBpFCLCH2973ueiKXR5qDimZynp7j_SGWT_haP-I4qWT0GQGidbOJflBZ5chGNMGSFzwRNuRpbFw-OLmrXq5hnOkxbdjF5PrQf1OdXD7cgQ
contexts:
#context info about mgmt-cluster
- context:
    cluster: lke49033
    namespace: default
    user: lke49033-admin
  name: lke49033-ctx
#context info about cluster-1
- context:
    cluster: lke49034
    namespace: default
    user: lke49034-admin
  name: lke49034-ctx
#context info about cluster-2
- context:
    cluster: lke49035
    namespace: default
    user: lke49035-admin
  name: lke49035-ctx
#current context (mgmt-cluster)
current-context: lke49033-ctx
```
Once we wrietten the new kubeconfig file, export the file:
    export KUBECONFIG=kubeconfig.yaml 
From now we can work across the cluster

### Exporting cluster's name and context into 

To take the list of the name and the context of the cluster run the following comand:

    kubectl config get-contexts
```
CURRENT   NAME           CLUSTER    AUTHINFO         NAMESPACE
*         lke49033-ctx   lke49033   lke49033-admin   default
          lke49034-ctx   lke49034   lke49034-admin   default
          lke49035-ctx   lke49035   lke49035-admin   default

```
The CLUSTER col stands for the name of the clsuter instead the NAME col stands for the context of the cluster. Copy them and exoport.
```
export MGMT_CONTEXT=lke49061-ctx
export REMOTE_CONTEXT1=lke49062-ctx
export REMOTE_CONTEXT2=lke49063-ctx
```
```
export MGMT_CLUSTER=lke49061
export REMOTE_CLUSTER1=lke49062
export REMOTE_CLUSTER2=lke49063
```
### Add your Gloo Mesh Enterprise license
Gloo Mesh Enterprise is a multicluster and multimesh management plane that is based on hardened, open-source projects like Envoy and Istio. With Gloo Mesh, you can unify the configuration, operation, and visibility of service-to-service connectivity across your distributed applications.

```
export GLOO_MESH_LICENSE_KEY=eyJleHAiOjE2NDI3MjMyMDAsImlhdCI6MTY0MDEzMTIwMCwiayI6IjBEd2FjQSIsImx0IjoidHJpYWwiLCJwcm9kdWN0IjoiZ2xvby1tZXNoIn0.myd3C8HtHF88E6ZkHrX2pceLKa53Uk9aAVJZhOUKzHQ
```

### Set and install the Istio into remote clusters

Deploy Istio to remote clusters for use in a production Gloo Mesh Enterprise environment.

    export ISTIO_VERSION=1.11.4



Install istio and export the path into bin folder

    curl -L https://istio.io/downloadIstio | sh -

    export PATH=$PWD/bin:$PATH

### Install meshctl 
```
curl -sL https://run.solo.io/meshctl/install | sh    

export PATH=$HOME/.gloo-mesh/bin:$PATH
```

### INSTALLARE ISTIO SUI CLUSTER 1 E 2
By installing Istio into remote clusters before you install the Gloo Mesh management plane, your Istio service meshes can be immediately discovered when you register the remote clusters.

Install istio in clsuter-1
```

CLUSTER_NAME=$REMOTE_CLUSTER1
cat << EOF | istioctl install -y --context $REMOTE_CONTEXT1 -f -
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  name: gloo-mesh-istio
  namespace: istio-system
spec:
  # only the control plane components are installed (https://istio.io/latest/docs/setup/additional-setup/config-profiles/)
  profile: minimal
  # Solo.io Istio distribution repository
  hub: gcr.io/istio-enterprise
  # Solo.io Gloo Mesh Istio tag
  tag: ${ISTIO_VERSION}

  meshConfig:
    # enable access logging to standard output
    accessLogFile: /dev/stdout

    defaultConfig:
      # wait for the istio-proxy to start before application pods
      holdApplicationUntilProxyStarts: true
      # enable Gloo Mesh metrics service (required for Gloo Mesh Dashboard)
      envoyMetricsService:
        address: enterprise-agent.gloo-mesh:9977
       # enable GlooMesh accesslog service (required for Gloo Mesh Access Logging)
      envoyAccessLogService:
        address: enterprise-agent.gloo-mesh:9977
      proxyMetadata:
        # Enable Istio agent to handle DNS requests for known hosts
        # Unknown hosts will automatically be resolved using upstream dns servers in resolv.conf
        # (for proxy-dns)
        ISTIO_META_DNS_CAPTURE: "true"
        # Enable automatic address allocation (for proxy-dns)
        ISTIO_META_DNS_AUTO_ALLOCATE: "true"
        # Used for gloo mesh metrics aggregation
        # should match trustDomain (required for Gloo Mesh Dashboard)
        GLOO_MESH_CLUSTER_NAME: ${CLUSTER_NAME}

    # Set the default behavior of the sidecar for handling outbound traffic from the application.
    outboundTrafficPolicy:
      mode: ALLOW_ANY
    # The trust domain corresponds to the trust root of a system. 
    # For Gloo Mesh this should be the name of the cluster that cooresponds with the CA certificate CommonName identity
    trustDomain: ${CLUSTER_NAME}
  components:
    ingressGateways:
    # enable the default ingress gateway
    - name: istio-ingressgateway
      enabled: true
      k8s:
        service:
          type: LoadBalancer
          ports:
            # health check port (required to be first for aws elbs)
            - name: status-port
              port: 15021
              targetPort: 15021
            # main http ingress port
            - port: 80
              targetPort: 8080
              name: http2
            # main https ingress port
            - port: 443
              targetPort: 8443
              name: https
            # Port for gloo-mesh multi-cluster mTLS passthrough (Required for Gloo Mesh east/west routing)
            - port: 15443
              targetPort: 15443
              # Gloo Mesh looks for this default name 'tls' on an ingress gateway
              name: tls
    pilot:
      k8s:
        env:
         # Allow multiple trust domains (Required for Gloo Mesh east/west routing)
          - name: PILOT_SKIP_VALIDATE_TRUST_DOMAIN
            value: "true"
  values:
    # https://istio.io/v1.5/docs/reference/config/installation-options/#global-options
    global:
      # needed for connecting VirtualMachines to the mesh
      network: ${CLUSTER_NAME}
      # needed for annotating istio metrics with cluster (should match trust domain and GLOO_MESH_CLUSTER_NAME)
      multiCluster:
        clusterName: ${CLUSTER_NAME}
EOF

```
Install istio in cluster-2
```

CLUSTER_NAME=$REMOTE_CLUSTER2
cat << EOF | istioctl install -y --context $REMOTE_CONTEXT2 -f -
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  name: gloo-mesh-istio
  namespace: istio-system
spec:
  # only the control plane components are installed (https://istio.io/latest/docs/setup/additional-setup/config-profiles/)
  profile: minimal
  # Solo.io Istio distribution repository
  hub: gcr.io/istio-enterprise
  # Solo.io Gloo Mesh Istio tag
  tag: ${ISTIO_VERSION}

  meshConfig:
    # enable access logging to standard output
    accessLogFile: /dev/stdout

    defaultConfig:
      # wait for the istio-proxy to start before application pods
      holdApplicationUntilProxyStarts: true
      # enable Gloo Mesh metrics service (required for Gloo Mesh Dashboard)
      envoyMetricsService:
        address: enterprise-agent.gloo-mesh:9977
       # enable GlooMesh accesslog service (required for Gloo Mesh Access Logging)
      envoyAccessLogService:
        address: enterprise-agent.gloo-mesh:9977
      proxyMetadata:
        # Enable Istio agent to handle DNS requests for known hosts
        # Unknown hosts will automatically be resolved using upstream dns servers in resolv.conf
        # (for proxy-dns)
        ISTIO_META_DNS_CAPTURE: "true"
        # Enable automatic address allocation (for proxy-dns)
        ISTIO_META_DNS_AUTO_ALLOCATE: "true"
        # Used for gloo mesh metrics aggregation
        # should match trustDomain (required for Gloo Mesh Dashboard)
        GLOO_MESH_CLUSTER_NAME: ${CLUSTER_NAME}

    # Set the default behavior of the sidecar for handling outbound traffic from the application.
    outboundTrafficPolicy:
      mode: ALLOW_ANY
    # The trust domain corresponds to the trust root of a system. 
    # For Gloo Mesh this should be the name of the cluster that cooresponds with the CA certificate CommonName identity
    trustDomain: ${CLUSTER_NAME}
  components:
    ingressGateways:
    # enable the default ingress gateway
    - name: istio-ingressgateway
      enabled: true
      k8s:
        service:
          type: LoadBalancer
          ports:
            # health check port (required to be first for aws elbs)
            - name: status-port
              port: 15021
              targetPort: 15021
            # main http ingress port
            - port: 80
              targetPort: 8080
              name: http2
            # main https ingress port
            - port: 443
              targetPort: 8443
              name: https
            # Port for gloo-mesh multi-cluster mTLS passthrough (Required for Gloo Mesh east/west routing)
            - port: 15443
              targetPort: 15443
              # Gloo Mesh looks for this default name 'tls' on an ingress gateway
              name: tls
    pilot:
      k8s:
        env:
         # Allow multiple trust domains (Required for Gloo Mesh east/west routing)
          - name: PILOT_SKIP_VALIDATE_TRUST_DOMAIN
            value: "true"
  values:
    # https://istio.io/v1.5/docs/reference/config/installation-options/#global-options
    global:
      # needed for connecting VirtualMachines to the mesh
      network: ${CLUSTER_NAME}
      # needed for annotating istio metrics with cluster (should match trust domain and GLOO_MESH_CLUSTER_NAME)
      multiCluster:
        clusterName: ${CLUSTER_NAME}
EOF


```


### Install Gloo Mesh Enterprise in the management cluster 
Install the Gloo Mesh Enterprise management components into your management cluster. The management components serve as the control plane where you define all service mesh configurations that you want Gloo Mesh to enforce across clusters and service meshes. The control plane also aggregates all of the discovered Istio service mesh components into the simplified Gloo Mesh API Mesh, Workload, and Destination custom resources.

    meshctl install enterprise --kubecontext=$MGMT_CONTEXT --license $GLOO_MESH_LICENSE_KEY

Verify the that all the pods ar ready:

    kubectl get pods -n gloo-mesh --context $MGMT_CONTEXT

Verify that the management plane is correctly installed. This check might take a few seconds to complete.

    meshctl check server --kubecontext $MGMT_CONTEXT




### Register remote clusters 

The relay server is exposed by the enterprise-networking LoadBalancer service. When you register remote clusters to be managed by Gloo Mesh Enterprise, a deployment named enterprise-agent is created on each remote cluster to run a relay agent. Each relay agent is exposed by an enterprise-agent ClusterIP service, from which all communication is outbound to the relay server on the management cluster.
1. In the management cluster, find the external address that was assigned by your cloud provider to the enterprise-networking LoadBalancer service. When you register the remote clusters in subsequent steps, the enterprise-agent relay agent in each cluster accesses this address via a secure connection. Note that it might take a few minutes for your cloud provider to assign an external address to the LoadBalancer.
```
   ENTERPRISE_NETWORKING_DOMAIN=$(kubectl get svc -n gloo-mesh enterprise-networking --context $MGMT_CONTEXT -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
   ENTERPRISE_NETWORKING_PORT=$(kubectl -n gloo-mesh get service enterprise-networking --context $MGMT_CONTEXT -o jsonpath='{.spec.ports[?(@.name=="grpc")].port}')
   ENTERPRISE_NETWORKING_ADDRESS=${ENTERPRISE_NETWORKING_DOMAIN}:${ENTERPRISE_NETWORKING_PORT}
   echo $ENTERPRISE_NETWORKING_ADDRESS
   
```
2. Register cluster-1 with the management plane. If you installed the management plane insecurely, include the --relay-server-insecure=true flag in this command.
```
meshctl cluster register enterprise \
  --mgmt-context=$MGMT_CONTEXT \
  --remote-context=$REMOTE_CONTEXT1 \
  --relay-server-address $ENTERPRISE_NETWORKING_ADDRESS \
  $REMOTE_CLUSTER1

```
3. Register cluster-2 with the management plane. If you installed the management plane insecurely, include the --relay-server-insecure=true flag in this command.
```
meshctl cluster register enterprise \
  --mgmt-context=$MGMT_CONTEXT \
  --remote-context=$REMOTE_CONTEXT2 \
  --relay-server-address $ENTERPRISE_NETWORKING_ADDRESS \
  $REMOTE_CLUSTER2

```
4. Verify that each remote cluster is successfully registered with Gloo Mesh.
    kubectl get kubernetescluster -n gloo-mesh --context $MGMT_CONTEXT
```
NAME           AGE
cluster-1      27s
cluster-2      23s
```
5. Verify that Gloo Mesh successfully discovered the Istio service meshes in each remote cluster.
    kubectl get mesh -n gloo-mesh --context $MGMT_CONTEXT
```
NAME                            AGE
istiod-istio-system-cluster-1   68s
istiod-istio-system-cluster-2   28s
```
Now that Gloo Mesh Enterprise is installed in the management cluster, the remote clusters are registered with the management plane, and the Istio meshes in the remote clusters are discovered by Gloo Mesh, your Gloo Mesh Enterprise setup is complete!

### Create a virtual mesh 
Bootstrap connectivity between the Istio service meshes in each remote cluster by creating a VirtualMesh. When you create a VirtualMesh resource in the management cluster, each service mesh in the remote clusters is configured with certificates that share a common root of trust. After trust is established, the virtual mesh configuration facilitates cross-cluster communications by federating services so that they are accessible across clusters.
1. Create a VirtualMesh resource named virtual-mesh in the gloo-mesh namespace of the management cluster.
```

kubectl apply --context $MGMT_CONTEXT -f - << EOF
apiVersion: networking.mesh.gloo.solo.io/v1
kind: VirtualMesh
metadata:
  name: virtual-mesh
  namespace: gloo-mesh
spec:
  mtlsConfig:
    # Note: Do NOT use this autoRestartPods setting in production!!
    autoRestartPods: true
    # automatically generate CA certificates for istiod deployments
    shared:
      rootCertificateAuthority:
        generated: {}
  federation:
    # federate all Destinations to all external meshes
    selectors:
    - {}
  # Disable global access policy enforcement for demonstration purposes.
  globalAccessPolicy: DISABLED
  meshes:
  - name: istiod-istio-system-${REMOTE_CLUSTER1}
    namespace: gloo-mesh
  - name: istiod-istio-system-${REMOTE_CLUSTER2}
    namespace: gloo-mesh
EOF

```
2. Verify that the virtual mesh is created and your services meshes are configured for multicluster traffic.
    kubectl get virtualmesh -n gloo-mesh virtual-mesh -oyaml --context $MGMT_CONTEXT

In the status section of the output, ensure that each service mesh and the virtual mesh have a state of ACCEPTED.

### Deploy Bookinfo across clustersand Route multicluster traffic

Start by deploying different versions of the Bookinfo sample app to both of the remote clusters. cluster-1 runs the app with versions 1 and 2 of the reviews service (reviews-v1 and reviews-v2), and cluster-2 runs version 3 of the reviews service (reviews-v3).

```
# create a bookinfo namespace to organize your demo resources
kubectl --context $REMOTE_CONTEXT1 create ns bookinfo
# prepare the bookinfo namespace for Istio sidecar injection
kubectl --context $REMOTE_CONTEXT1 label namespace bookinfo istio-injection=enabled
# deploy bookinfo application components for all versions less than v3
kubectl --context $REMOTE_CONTEXT1 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'app,version notin (v3)'
# deploy all bookinfo service accounts
kubectl --context $REMOTE_CONTEXT1 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'account'
# configure ingress gateway to access bookinfo
kubectl --context $REMOTE_CONTEXT1 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/networking/bookinfo-gateway.yaml

```

Verify that the Bookinfo app is running in cluster-1.

    kubectl --context $REMOTE_CONTEXT1 get pods -n bookinfo

install bookinfo in cluster-2
```
# create a bookinfo namespace to organize your demo resources
kubectl --context $REMOTE_CONTEXT2 create ns bookinfo
# prepare the bookinfo namespace for Istio sidecar injection
kubectl --context $REMOTE_CONTEXT2 label namespace bookinfo istio-injection=enabled
# deploy reviews and ratings services
kubectl --context $REMOTE_CONTEXT2 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'service in (reviews)'
# deploy reviews-v3
kubectl --context $REMOTE_CONTEXT2 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'app in (reviews),version in (v3)'
# deploy ratings
kubectl --context $REMOTE_CONTEXT2 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'app in (ratings)'
# deploy reviews and ratings service accounts
kubectl --context $REMOTE_CONTEXT2 -n bookinfo apply -f https://raw.githubusercontent.com/istio/istio/$ISTIO_VERSION/samples/bookinfo/platform/kube/bookinfo.yaml -l 'account in (reviews, ratings)'

```
Verify that the Bookinfo app is running on cluster-2.

    kubectl --context $REMOTE_CONTEXT2 get pods -n bookinfo


Get the address of the Istio ingress gateway on cluster-1.

```
   CLUSTER_1_INGRESS_ADDRESS=$(kubectl --context $REMOTE_CONTEXT1 get svc -n istio-system istio-ingressgateway -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
   echo http://$CLUSTER_1_INGRESS_ADDRESS/productpage
   
```
open http://$CLUSTER_1_INGRESS_ADDRESS/productpage

Refresh the page a few times to see the black stars in the Book Reviews column appear and disappear. The presence of black stars represents reviews-v1 and the absence of black stars represents reviews-v2.
![image info](./Images/star-rotation.png)

### Shift traffic across clusters 
In order for the product-page service on cluster-1 to access reviews-v3 on cluster-2, you can use Gloo Mesh to route traffic across the remote clusters. You can route traffic to reviews-v3 by creating a Gloo Mesh TrafficPolicy resource that diverts 75% of reviews traffic to the reviews-v3 service.

```
cat << EOF | kubectl --context $MGMT_CONTEXT apply -f -
apiVersion: networking.mesh.gloo.solo.io/v1
kind: TrafficPolicy
metadata:
  namespace: gloo-mesh
  name: simple
spec:
  sourceSelector:
  - kubeWorkloadMatcher:
      namespaces:
      - bookinfo
  destinationSelector:
  - kubeServiceRefs:
      services:
        - clusterName: ${REMOTE_CLUSTER1}
          name: reviews
          namespace: bookinfo
  policy:
    trafficShift:
      destinations:
        - kubeService:
            clusterName: ${REMOTE_CLUSTER2}
            name: reviews
            namespace: bookinfo
            subset:
              version: v3
          weight: 75
        - kubeService:
            clusterName: ${REMOTE_CLUSTER1}
            name: reviews
            namespace: bookinfo
            subset:
              version: v1
          weight: 15
        - kubeService:
            clusterName: ${REMOTE_CLUSTER1}
            name: reviews
            namespace: bookinfo
            subset:
              version: v2
          weight: 10
EOF
```
Now, the red stars for reviews-v3 are shown in the book reviews.

### LANCIARE LA DASHBOARD 
```
meshctl dashboard --kubecontext $MGMT_CONTEXT
```
![image info](./images/../Images/dashboard.png)
Click the Graph tab to see the visualization of 75% of traffic flowing to reviews-v3, 15% to reviews-v1, and 10% to reviews-v2, as defined by your traffic policy.
![image infp](./images/../Images/Schermata%202022-01-10%20alle%2017.48.28.png)

## FAILOVER CASE

In the event that a cluster due to overload is unable to respond to requests, it is possible to create a policy for traffic to be sent directly to the healthy cluster.
1. Create a Virtual Destination
```
kubectl --context $MGMT_CONTEXT apply -f - << EOF
apiVersion: networking.enterprise.mesh.gloo.solo.io/v1beta1
kind: VirtualDestination
metadata:
  name: bookinfo-global
  namespace: gloo-mesh
spec:
  hostname: reviews.global
  port:
    number: 9080
    protocol: http
  localized:
    outlierDetection:
      consecutiveErrors: 1
      maxEjectionPercent: 100
      interval: 5s
      baseEjectionTime: 120s
    destinationSelectors:
    - kubeServiceMatcher:
        labels:
          app: reviews
  virtualMesh:
    name: virtual-mesh
    namespace: gloo-mesh
EOF

```
2. Create a Failover TrafficShiftPolicy
```
kubectl --context $MGMT_CONTEXT apply -f - << EOF
apiVersion: networking.mesh.gloo.solo.io/v1
kind: TrafficPolicy
metadata:
  name: reviews-shift-failover
  namespace: gloo-mesh
spec:
  destinationSelector:
  - kubeServiceRefs:
      services:
      - clusterName: $REMOTE_CLUSTER1
        name: reviews
        namespace: bookinfo
  policy:
    trafficShift:
      destinations:
      - virtualDestination:
          name: bookinfo-global
          namespace: gloo-mesh
EOF
```
Scale down reviews v1 & v2 in cluster1 to simulate a failover scenario:
```
kubectl scale deploy reviews-v1 --replicas=0 --context $REMOTE_CONTEXT1 -n bookinfo                                                   ─╯
kubectl scale deploy reviews-v2 --replicas=0 --context $REMOTE_CONTEXT1 -n bookinfo                                                   ─╯
```
When the reviews v1 and v2 service deployments fail in cluster1, the productpage service in cluster1 is automatically routed to the reviews v3 service in cluster2 automatically without any manual intervention.

![](./Images/bookinfo-v3.png)
![](./Images/Schermata%202022-01-10%20alle%2017.40.06.png)

Scale up reviews v1 & v2 in cluster1 to simulate a cluster-1 fix scenario:
```
kubectl scale deploy reviews-v1 --replicas=0 --context $REMOTE_CONTEXT1 -n bookinfo                                                   ─╯
kubectl scale deploy reviews-v2 --replicas=0 --context $REMOTE_CONTEXT1 -n bookinfo                                                   ─╯
```
