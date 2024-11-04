
# Build Release Assets

This GitHub Action builds release assets by checking out the Platomo build repository, installing dependencies, and executing the release build. Optionally, it can save the build artifacts for later use.

## Usage

### Inputs

- **`platomo-token`** (required): Access token for the Platomo Builder repository.
- **`package-version`** (required): Version number of the package to be built.
- **`save-artifacts`** (optional): Indicates if the build artifacts should be archived and saved.

### Example Workflow

Here’s an example of how to use the `Build Release Assets` action in a workflow:

```yaml
name: Build Release Assets

on:
  push:
    tags:
      - 'v*.*.*'

jobs:
  build-release:
    runs-on: ubuntu-latest

    steps:
      - name: Build Release Assets
        uses: ./.github/actions/build-release-assets
        with:
          platomo-token: ${{ secrets.PLATOMO_TOKEN }}
          package-version: '1.2.3'
          save-artifacts: true
```

## How It Works

1. **Check Out Repository**: The action checks out the `platomo-build` repository using the provided access token.
2. **Install Dependencies**: Installs dependencies specified in `requirements.txt` and `requirements-dev.txt` if they exist.
3. **Build Release Assets**: Runs the `build.py` script in the Platomo repository to generate release assets based on the specified package version.
4. **Archive Results**: Optionally saves build results as artifacts, if `save-artifacts` is set to `true`.

### Notes

- Ensure the `platomo-token` has permissions to access the `platomo-build` repository.
- Specify the correct package version for each release.
- If `save-artifacts` is set to `true`, the build results will be archived as `build-results` under the `dist` directory.
