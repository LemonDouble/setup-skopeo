# skopeo-setup-action

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A GitHub Action that sets up [Skopeo](https://github.com/containers/skopeo) on your runner. 

This action downloads and installs the Skopeo binary based on the runner's architecture, and also fetches the default container image policy file.

## Features

- Updates package lists and installs `wget`
- Determines system architecture (supports `amd64` & `arm64`)
- Downloads the appropriate Skopeo binary from [lework/skopeo-binary](https://github.com/lework/skopeo-binary/releases)
- Sets the proper executable permissions on Skopeo
- Downloads and configures the default container policy file

## Compatibility

⚠️ This action has been designed and tested specifically for Debian and Ubuntu environments. It may not work properly on other Linux distributions.

## Usage

Integrate this action into your workflow file as follows:

```yaml
jobs:
  setup:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Skopeo
        uses: LemonDouble/setup-skopeo@v1.0.0
        with:
          version: v1.18.0   # Optional: defaults to 'v1.18.0'
```

## Inputs

| Input    | Description                                | Required | Default    |
| -------- | ------------------------------------------ | -------- | ---------- |
| version  | Version of Skopeo to install               | No       | v1.18.0    |

- You can find supported version on this [Link](https://github.com/lework/skopeo-binary/blob/master/version.txt)

## How It Works

1. **Setup Items**:  
   Updates the package list and installs `wget` which is required for downloading files.

2. **Determine Architecture**:  
   Evaluates the system architecture:
   - `x86_64` is mapped to `amd64`
   - `aarch64` or `arm64` is mapped to `arm64`  
   If the architecture is unsupported, the action exits with an error.

3. **Download Skopeo Binary**:  
   Downloads the Skopeo binary tailored for the runner's architecture and places it in `/usr/bin/skopeo`.

4. **Set Execute Permissions**:  
   Sets the executable permissions on the downloaded binary.

5. **Download Default Policy**:  
   Retrieves the default container policy JSON and stores it under `~/.config/containers/policy.json`.

## Customization

Feel free to modify this action to suit your workflow needs:
- Also Pull Requests are welcome. Even if it's your first contribution, feel free to open one.

## License

This project is licensed under the [MIT License](LICENSE).

## Author

Contact: [contact@lemondouble.com](mailto:contact@lemondouble.com)

---

Happy container managing!