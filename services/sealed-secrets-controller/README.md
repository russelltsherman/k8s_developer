# Sealed Secrets

## references

[Home](https://sealed-secrets.netlify.app)
[Github](https://github.com/bitnami-labs/sealed-secrets)

## usage

Once it is running, you can retrieve the generated public key certificate using kubeseal and store it on your local disk.

```sh
kubeseal --fetch-cert > public-key-cert.pem
```

You can then create a Secret and seal it with kubeseal.
This example will use the manifest detailed at the start of this section, but you can change the key-value pairs under the data field as you see fit.

```sh
kubeseal --cert=public-key-cert.pem --format=yaml < secret.yaml > sealed-secret.yaml
```

The generated output will look something like this:

```yaml
apiVersion: bitnami.com/v1alpha1
kind: SealedSecret
metadata:
  creationTimestamp: null
  name: my-secret
  namespace: default
spec:
  encryptedData:
    password: AgBvA5WMunIZ5rF9...
    username: AgCCo8eSORsCbeJSoRs/...
  template:
    data: null
    metadata:
      creationTimestamp: null
      name: my-secret
      namespace: default
    type: Opaque
```

This manifest can be used to create the Sealed Secret in your cluster with kubectl and afterward stored in a git repository without the concern of any individual accessing the original values.

```sh
kubectl create -f sealed-secret.yaml
```

You can then proceed to review the secret and fetch its values.

```sh
kubectl get secret my-secret -o jsonpath="{.data.user}" | base64 --decode
kubectl get secret my-secret -o jsonpath="{.data.password}" | base64 --decode
```
