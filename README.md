# ElseMesh experimental preview publisher

**[Open the experimental preview](https://lozknowles.github.io/ElseMesh-preview/)**

This repository publishes a static WebGPU test build from the exact
[`lozknowles/ElseMesh` draft PR #6](https://github.com/lozknowles/ElseMesh/pull/6)
commit pinned in [the Pages workflow](.github/workflows/deploy-preview.yml).
It contains a publisher recipe, not a second game source tree. The served
`preview-build.json` states the exact source commit and preview scope.

The preview lets a friend try the island while the source is reviewed. It
does **not** run an internet multiplayer server or qualify live cross-world
travel. The visible banner and separate browser save names distinguish it
from the [existing public build](https://lozknowles.github.io/ElseMesh/).

To contribute weather changes, inspect draft PR #6 and its feature/mist-thunderstorms branch. The default game branch remains unchanged. The weather preview is experimental: lightning timing, underwater transitions and smoothness are not qualified.

## Update or roll back

Normal publishing now uses the prebuilt `gh-pages` branch with `.nojekyll`.
Build the exact source commit pinned in `.github/workflows/deploy-preview.yml`
in a clean isolated checkout, run `npm run build` and `node ../elsemesh-preview-publisher/tools/preview/stage-static-preview.mjs`,
inspect the resulting publication scan and manifest, then commit only
`artifacts/preview-site` contents to `gh-pages`. Pages uses Deploy from a branch,
`gh-pages`, root. No custom CI build is required.

The old source-build workflow is manual-only as a fallback. If using it, switch
Pages back to GitHub Actions before running it. Normal updates do not use this workflow.

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

## Stager provenance and weather candidate

The publisher-owned staging and generic privacy scanner are derived from ElseMesh f2afd7f2858c5cd8080e0f3514a3934e29d0daa8; the banner source link now points to draft PR #6. Their MIT notice is in tools/UPSTREAM-LICENSE.txt. The game commit is pinned separately in the workflow and the live preview-build.json. The normal gh-pages path requires no custom CI build. The stager adds the storage wrapper before game startup, including namespacing the weather preference key. Snapshot21b43a5 is the earlier preview rollback point.
