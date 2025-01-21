### Baseline checklist for ensuring security in Kubernetes clusters ###
# 2025_01_21
# Ref: https://kubernetes.io/docs/concepts/security/security-checklist/

- [ ] Authentication & Authorization
  - [ ] system:masters group is not used for user or component authentication after bootstrapping.
  - [ ] The kube-controller-manager is running with --use-service-account-credentials enabled.
  - [ ] The root certificate is protected (either an offline CA, or a managed online CA with effective access controls).
  - [ ] Intermediate and leaf certificates have an expiry date no more than 3 years in the future.
  - [ ] A process exists for periodic access review, and reviews occur no more than 24 months apart.
  - [ ] The Role Based Access Control Good Practices are followed for guidance related to authentication and authorization.

- [ ] Pod security
  - [ ] RBAC rights to create, update, patch, delete workloads is only granted if necessary.
  - [ ] Appropriate Pod Security Standards policy is applied for all namespaces and enforced.
  - [ ] Memory limit is set for the workloads with a limit equal or inferior to the request.
  - [ ] CPU limit might be set on sensitive workloads.
  - [ ] For nodes that support it, Seccomp is enabled with appropriate syscalls profile for programs.
  - [ ] For nodes that support it, AppArmor or SELinux is enabled with appropriate profile for programs.

- [ ] Logs and auditing
  - [ ] Audit logs, if enabled, are protected from general access.

- [ ] Pod placement
  - [ ] Pod placement is done in accordance with the tiers of sensitivity of the application.
  - [ ] Sensitive applications are running isolated on nodes or with specific sandboxed runtimes.

- [ ] Secrets
  - [ ] ConfigMaps are not used to hold confidential data.
  - [ ] Encryption at rest is configured for the Secret API.
  - [ ] If appropriate, a mechanism to inject secrets stored in third-party storage is deployed and available.
  - [ ] Service account tokens are not mounted in pods that don't require them.
  - [ ] Bound service account token volume is in-use instead of non-expiring tokens.

- [ ] Images
  - [ ] Minimize unnecessary content in container images.
  - [ ] Container images are configured to be run as unprivileged user.
  - [ ] References to container images are made by sha256 digests (rather than tags) or the provenance of the image is validated by verifying the image's digital signature at deploy time via admission control.
  - [ ] Container images are regularly scanned during creation and in deployment, and known vulnerable software is patched.

- [ ] Admission controllers
  - [ ] An appropriate selection of admission controllers is enabled.
  - [ ] A pod security policy is enforced by the Pod Security Admission or/and a webhook admission controller.
  - [ ] The admission chain plugins and webhooks are securely configured.

