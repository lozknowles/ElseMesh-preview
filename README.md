# ElseMesh experimental preview publisher

**[Open the experimental preview](https://lozknowles.github.io/ElseMesh-preview/)**

This repository publishes a static WebGPU test build from the exact
[`lozknowles/ElseMesh` draft PR #5](https://github.com/lozknowles/ElseMesh/pull/5)
commit pinned in [the Pages workflow](.github/workflows/deploy-preview.yml).
It contains a publisher recipe, not a second game source tree. The served
`preview-build.json` states the exact source commit and preview scope.

The preview lets a friend try the island while the source is reviewed. It
does **not** run an internet multiplayer server or qualify live cross-world
travel. The visible banner and separate browser save names distinguish it
from the [existing public build](https://lozknowles.github.io/ElseMesh/).

To contribute game changes, use the PR #5 source branch
`feature/network-federation-hardening` in the main repository. Fork it and
propose a pull request, or ask the maintainer for collaborator access if direct
pushes are needed. See the main repository's [README](https://github.com/lozknowles/ElseMesh/blob/feature/network-federation-hardening/README.md),
[changelog](https://github.com/lozknowles/ElseMesh/blob/feature/network-federation-hardening/CHANGELOG.md),
and [qualification status](https://github.com/lozknowles/ElseMesh/blob/feature/network-federation-hardening/docs/EXPERIMENTAL-PREVIEW.md).

## Update or roll back

Normal publishing now uses the prebuilt `gh-pages` branch with `.nojekyll`.
Build the exact source commit pinned in `.github/workflows/deploy-preview.yml`
in a clean isolated checkout, run `npm run build` and `npm run stage:static-preview`,
inspect the resulting publication scan and manifest, then commit only
`artifacts/preview-site` contents to `gh-pages`. Pages uses Deploy from a branch,
`gh-pages`, root. No custom CI build is required.

The old source-build workflow is manual-only as a fallback. If using it, switch
Pages back to GitHub Actions before running it. It contains GPU-dependent checks
that may fail on runners without a working WebGPU adapter.

Rollback uses an earlier reviewed static commit on `gh-pages`, committed normally;
do not force-push. To retire the preview, disable Pages. These operations do not
change the production ElseMesh site or either game source branch.

## Preview repair (2026-10-21)

The URL returned 404 with no successful deployment. The previous custom workflow
failed because its runner had no WebGPU adapter; the next run was cancelled.
The pinned source was built locally without game-source edits and staged with
the existing publication scanner, experimental banner and isolated browser-storage
prefix. No live federation service is included. The private standalone world
builder remains a different repository.

Build-tool dependency audit reported high-severity advisories in Vite and
source-map-js at this historical pin. They were not upgraded during this repair;
neither the Vite development server nor node_modules is published. Interactive
game acceptance is separate from successful deployment.
