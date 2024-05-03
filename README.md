# stunning-broccoli

This repository contains [main.go](main.go), which is the code for an example program.

It also contains [build-attested-release.yml](.github/workflows/build-attested-release.yml), which is a GitHub workflow that checks out the code, builds cross-platform binaries, creates an archive containing the binaries, creates an attestation for that archive, and then publishes a release.

## Building a release

A build can be triggered by running the action as a workflow dispatch.

## Verifying the attestation

The release artifact binary can be downloaded and the the attestation verified using the `gh` client.

For example:
```
$ curl -sLO https://github.com/finnigja/stunning-broccoli/releases/download/f1350b67/stunning-broccoli-f1350b67.tar.gz
$ gh attestation verify ./stunning-broccoli-f1350b67.tar.gz -o finnigja
Loaded digest sha256:394a35508a9e5c154231f267d0f1c61f752b72c2a91c88aa4fe9e052545e3d94 for file://stunning-broccoli-f1350b67.tar.gz
Loaded 1 attestation from GitHub API
✓ Verification succeeded!

sha256:394a35508a9e5c154231f267d0f1c61f752b72c2a91c88aa4fe9e052545e3d94 was attested by:
REPO                        PREDICATE_TYPE                  WORKFLOW
finnigja/stunning-broccoli  https://slsa.dev/provenance/v1  .github/workflows/build-attested-release.yml@refs/heads/main
```

## About the attestation feature

For more information about the GitHub artifact attestation feature:
* https://github.blog/2024-05-02-introducing-artifact-attestations-now-in-public-beta/
* https://docs.github.com/en/actions/security-guides/using-artifact-attestations-to-establish-provenance-for-builds
