# Cert Manager Webhook

https://cert-manager.io/docs/concepts/webhook/

## Usage

The `namespace` you deploy this into will need to be written into various fields so that the admission webhook works.
Use the following kustomization snippet to do so:
```yaml
replacements:
  - source:
      kind: Deployment
      name: cert-manager-webhook
      fieldPath: metadata.namespace
    targets:
      - select:
          kind: MutatingWebhookConfiguration
        fieldPaths:
          - metadata.annotations.[cert-manager.io/inject-ca-from-secret]
        options:
          delimiter: /
      - select:
          kind: ValidatingWebhookConfiguration
        fieldPaths:
          - metadata.annotations.[cert-manager.io/inject-ca-from-secret]
        options:
          delimiter: /
```
