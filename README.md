# Rancher Government Carbide — Public Artifacts

This repository is the public distribution point for artifacts related to
Rancher Government Carbide. If you need something public from Carbide — most commonly
the signing key used to verify images and artifacts pulled from the Carbide registry —
you can get it here.

Full documentation: **[docs.ranchercarbide.dev](https://docs.ranchercarbide.dev)**

Nothing in this repository is sensitive. It is intentionally public so that customers,
air-gapped operators, and automated pipelines can fetch these files without credentials.

## Contents

| File | Description |
| --- | --- |
| `carbide-key.pub` | Cosign public key used to verify signatures on artifacts published to the Carbide registry. |
| `carbide-key.pub.sha256` | SHA-256 checksum of `carbide-key.pub`, for confirming an authentic copy of the key. |
| `LICENSE` | Apache License 2.0 covering the contents of this repository. |

## Verifying Carbide artifacts

Carbide artifacts are signed with [cosign](https://docs.sigstore.dev/cosign/system_config/installation/).
Download the public key from this repository and use it to verify an image:

```bash
# Fetch the public key
curl -sSLO https://raw.githubusercontent.com/ranchergovernment/carbide/main/carbide-key.pub

# Verify an image from the Carbide registry
cosign verify --key carbide-key.pub <registry>/<image>:<tag>
```

A successful verification prints the verified signature payload. If verification fails,
do not use the artifact — reach out to Rancher Government support.

### Validating the key itself

Before trusting `carbide-key.pub`, confirm it matches the published checksum:

```bash
curl -sSLO https://raw.githubusercontent.com/ranchergovernment/carbide/main/carbide-key.pub
curl -sSLO https://raw.githubusercontent.com/ranchergovernment/carbide/main/carbide-key.pub.sha256

shasum -a 256 -c carbide-key.pub.sha256
# carbide-key.pub: OK
```

Current published checksum:

```
2e57896c49d007f88560c1cecf5473fede3ecb7a0156301df01b89e946088305  carbide-key.pub
```

## License

Licensed under the [Apache License, Version 2.0](LICENSE).
