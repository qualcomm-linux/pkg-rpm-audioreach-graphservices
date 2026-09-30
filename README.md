<!--
Copyright (c) Qualcomm Technologies, Inc. and/or its subsidiaries.
SPDX-License-Identifier: BSD-3-Clause
-->
# pkg-rpm-audioreach-graphservices

RPM packaging for
[audioreach-graphservices](https://github.com/Audioreach/audioreach-graphservices)
on CentOS Stream 10 (aarch64).

audioreach-graphservices provides cross-platform libraries (GSL and ACDB) for
managing audio graphs in the AudioReach framework, including setup, control,
data exchange, and calibration handling on Qualcomm platforms. The package is
maintained on the CentOS Stream 10 (`c10s`) branch and uses the shared GitHub
Actions build and release workflow.

---

## Repository Layout

The `c10s` branch contains the RPM packaging files:

| File | Purpose |
|---|---|
| `audioreach-graphservices.spec` | Builds the graph service runtime libraries and `-devel` subpackage. |
| `sources` | SHA-512 checksum for the upstream source archive. |
| `0001-*.patch` | Packaging patch applied during the build. |
| `README.md` | Package and repository documentation. |
| `LICENSE.txt` | License for the RPM packaging repository. |

The source archive is not committed to this repository. The spec file's
`Source0` points to the upstream release, and the checksum in `sources` is
verified before the RPM is built.

---

## Packages

- `audioreach-graphservices`: AudioReach graph service runtime libraries (GSL
  and ACDB) for managing audio graphs.
- `audioreach-graphservices-devel`: Library headers and pkg-config files for
  the shared libraries shipped in the `audioreach-graphservices` package.

---

## Updating the package version

This is the everyday workflow — **two edits on `c10s`, no tarball in git**:

1. Bump `Version:` in the spec (and the `Source0:` URL if its path changed).
2. Recompute the checksum for the new tarball:
   ```bash
   sha512sum --tag audioreach-graphservices-<newversion>.tar.gz > sources
   ```
3. Commit the spec + `sources`, open a PR (build verifies it), merge, then run
   **Release**. The first release fetches the new upstream tarball, verifies it,
   and caches it back to Artifactory automatically.

## License

This project is licensed under the BSD 3-Clause License. See [LICENSE.txt](LICENSE.txt) for the complete license text.
