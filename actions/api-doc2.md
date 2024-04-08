```yaml
name: Deploy API documentation

on:
  push:
    branches:
      - main

jobs:
  deploy-doc:
    if: ${{ github.event_name == 'push' }}
    name: Deploy API documentation
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Set up Homebrew
        id: set-up-homebrew
        uses: Homebrew/actions/setup-homebrew@master

      - name: Install Overalls dependencies
        run: |
          brew install speakeasy-api/homebrew-tap/speakeasy

      - name: Apply Overlays to customise OpenAPI
        working-directory: ./api
        run: |
          speakeasy overlay apply -s openapi.yaml -o overlays.yaml > openapi.public.yaml

      - name: Deploy API documentation
        run: <whatever command you use to deploy>
```
