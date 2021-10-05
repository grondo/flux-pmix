### flux-pmix

This repo contains a flux shell plugin for bootstrapping openmpi v5+
MPI executables.

The plugin is loaded by requesting it at job submission time with
the `-ompi=openmpi@5` option.

Typically this project would be configured with the same `--prefix` as
flux-core.  If that is not practical, for example in a spack environment,
then flux can be told to look elsewhere by setting `FLUX_SHELL_RC_PATH`, e.g.

```
FLUX_SHELL_RC_PATH=$prefix/etc/flux/shell/lua.d:$FLUX_SHELL_RC_PATH
```
where `$prefix` is the installation prefix of this project.

### license

SPDX-License-Identifier: LGPL-3.0

LLNL-CODE-76440
