# README for the project Update Custom Properties

**Update custom properties for all repos in an organization from a YAML file.**

This action uses the GitHub CLI to read values from `repo-properties.yaml` and update repos in the organization. This
can be useful for easily maintaining a single source of truth and a git-based history of updates to the
custom properties of the organization.

---

## 🚀 Getting Started

1. Add this GitHub Action to your workflow.
2. Run the workflow. The file `repo-properties.yaml` will automatically be parsed and all appropriate repo values
will be updated.

---

## Fine Grained Token Requirements

To run the action within your GitHub CI/CD pipeline you will need to create a
fine-grained token with the following permissions:

### Organization Permissions

- Read and Write access to repository custom properties

### Additional Information

- [GitHub API for custom property for an organization](https://docs.github.com/en/rest/orgs/custom-properties?apiVersion=2022-11-28#create-or-update-a-custom-property-for-an-organization)
- [Fine-grained personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token)
- The owner of the fine-grained token must have full administrative rights to the organization.

---

## 📦 Inputs

| Name                   | Description                                                       | Required | Default                |
|------------------------|-------------------------------------------------------------------|----------|------------------------|
| `token`                | GitHub Personal Access Token (Fine-Grained with: Repository custom properties `Read and Write` scope) | ✅ Yes    | —                      |
| `repo-properties.yaml` | File should be located in the root-level directory.               | ✅ Yes    | `repo-properties.yaml` |

---

## 🛠 Usage

```yaml
jobs:
  update-schema:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: PandasWhoCode/update-custom-properties@v1
        with:
          token: ${{ secrets.GH_CUSTOM_PROPERTIES_TOKEN }}
```

---

## Example custom_props.json

`custom_props.json`:
```yaml
org: PandasWhoCode
repositories:
  - name: my-example-repo
    last-date-modified: ""
    initial-ci-review-by-team: "pandas"
    initial-ci-review-date: "2025-04-07"
    initial-security-review-by-team: "admins"
    initial-security-review-date: "2025-04-15"
    last-security-review-by-team: "reviewers"
    last-security-review-date: "2025-05-01"
```

---

## 👤 Author

Andrew Brandt

[PandasWhoCode](https://pandaswhocode.com)

[andrew.brandt@pandaswhocode.com](mailto:andrew.brandt@pandaswhocode.com)

---