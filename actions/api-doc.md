Note: depends on bump CLI

```
name: Deploy documentation

on:
  push:
    branches:
      - main

jobs:
  deploy-doc:
    name: Deploy API doc on Bump.sh
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Apply overlay to API document
        run: |
          npx bump-cli overlay api/openapi.bundle.yaml api/overlays.yaml > api/openapi.public.yaml

      - name: Deploy API documentation
        uses: bump-sh/github-action@v1
        with:
          doc: partner-api
          token: ${{secrets.BUMP_TOKEN}}
          file: api/openapi.public.yaml
```
