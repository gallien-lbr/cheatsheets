# Kubernetes (K8s) and Helm Chart Notes

---

- The process involves taking the K8s YAML, making it variable, and versioning the code on Git.

- YAML modification includes updating the tag for container rebuild. Variables are stored in `nest-helm/xxx-values.yaml`.

- Goal: Deploying applications on K8s/Rancher, e.g., deploying version 2.3.1.

- Utilize liveness and readiness probes. Encountered deployment issues on CNOM.

- In "Apps" > "Installed apps," Helm-deployed apps like `drupalweb:2.3.1` are visible.

- Local deployment using `helm install`.

- CI: Create a package placed in Harbor. Harbor stores Helm charts at [Harbor Helm Charts](https://example-domain.fr/harbor/projects/99/helm-charts).

- Check the "values" tab in Harbor for `values.yaml`.

- HELM uses OCI standard. PODMAN is employed.

- No need for a database (`false`).

- Part of CI/CD is done in `drupal-deploy-helm`. The term `drupalweb` might work for various apps.

---

## Symfony / Angular: Example Deployment of "advent-calendar"

- Use `helm upgrade`.

- Deleting an app removes all related objects (ingress, deployments, etc.).

---

## Strategy: Starting from HELM and Attempting Deployment

- PVC for storage.

- Revision (e.g., DRUPAL release on sandbox) increments with each "helm upgrade."

- Chart version: `2.3.1`.

- When taking the Helm chart image: first deployment = `rev1`, second deployment = `rev2`.

- `--dry-run` (run without execution) provides YAML output.

---

## Projects and Repositories

- Drupalweb project: Helm chart build.

- Example project like CNOM assumes Docker images are built.

- Utilize HELM for deployment: [met-docker-deploy](https://example-domain.fr/bdx/pole-drupal/bordeaux-metropole/met-docker-deploy).

---

## Group Factory and Relevant Repositories

- [Group Factory](https://example-domain.fr/bdx/factory): Explore Helm templates and projects.

- Helm template for Drupal: [drupal-deploy](https://example-domain.fr/bdx/factory/helm-template/drupal-deploy) - Packages similar to Docker Compose.

- Example: [cnom/nest-deploy](https://example-domain.fr/bdx/pole-drupal/cnom/nest-deploy) - Uses Helm chart construction.

---

## Additional Considerations

- For MariaDB, prefer using a specific user over the root account.

- MariaDB in K8s "statefulset" at "/var/lib/mysql."

- Helm charts allow programming in GO within YAML.

