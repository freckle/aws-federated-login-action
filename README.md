# AWS Federated Login Action

Implements the credentials request described [here][blog].

[bloc]: https://awsteele.com/blog/2021/09/15/aws-federation-comes-to-github-actions.html

## Pre-requisites

You've deployed the resources described in the linked blog post and captured the
ARN of the Role you want your GitHub Action to assume.

You've set `AWS_ROLE_ARN` as a [secret][] in your repository.

[secret]: https://docs.github.com/en/actions/security-guides/encrypted-secrets

## Usage

```yaml
jobs:
  example:
    runs-on: ubuntu-latest

    permissions:
      id-token: write
      contents: read

    steps:
      - uses: freckle/aws-federated-login-action@v1
        with:
          aws-region: us-east-1
          aws-role-arn: ${{ secrets.AWS_ROLE_ARN }}

      - run: |
          aws sts get-caller-identity
```

## Inputs

See [`action.yml`](./action.yml).

## Outputs

None.

---

[LICENSE](./LICENSE)
