# stunning-broccoli

This repository contains [main.go](main.go), which is the code for an example program.

It also contains [build-attested-release.yml](.github/workflows/build-attested-release.yml), which is a GitHub workflow that checks out the code, builds cross-platform binaries, creates an archive containing the binaries, creates an attestation for that archive, and then publishes a release.

## Building a release

The workflow is configured to build when a new tag is pushed, with something like:
```
$ git tag v0.0.1 main -m "release v0.0.1"
$ git push origin tag v0.0.1
```

## Verifying the attestation

The release artifact binary can be downloaded and the the attestation verified using the `gh` client.

For example:
```
$ curl -sLO https://github.com/finnigja/stunning-broccoli/releases/download/93e64141/stunning-broccoli-93e64141.tar.gz
$ gh attestation verify ./stunning-broccoli-93e64141.tar.gz -o finnigja
Loaded digest sha256:8a1002fc62cbd7e52c5a5889c478fb6085f603e236e547765fa4efeaf90a02eb for file://stunning-broccoli-93e64141.tar.gz
Loaded 1 attestation from GitHub API
✓ Verification succeeded!

sha256:8a1002fc62cbd7e52c5a5889c478fb6085f603e236e547765fa4efeaf90a02eb was attested by:
REPO                        PREDICATE_TYPE                  WORKFLOW
finnigja/stunning-broccoli  https://slsa.dev/provenance/v1  .github/workflows/build-attested-release.yml@refs/heads/main
```

A JSON-formatted attestation with more detail can be obtained by adding `--format json` to the `gh attestation verify` command.

## About the attestation feature

For more information about the GitHub artifact attestation feature:
* https://github.blog/2024-05-02-introducing-artifact-attestations-now-in-public-beta/
* https://docs.github.com/en/actions/security-guides/using-artifact-attestations-to-establish-provenance-for-builds

## About the stunning broccoli

The fantastic piece of ASCII art packaged here came from [https://emojicombos.com/broccoli-ascii-art](https://emojicombos.com/broccoli-ascii-art).

