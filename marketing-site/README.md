# Voxletra marketing site

Complete Astro source staged for the future public repository `voxletra/voxletra.github.io` and URL `https://voxletra.github.io/`.

## Canonical planning

- Linear project: [github.com/voxletra](https://linear.app/denman/project/githubcomvoxletra-5528d72e4a7d)
- GitHub Project: [voxletra-project #1](https://github.com/orgs/voxletra/projects/1)
- Official clients: `voxletra/vxl-clients` (private)
- Shared interfaces: `voxletra/vxl-interfaces` (private)

## Client truth

The page uses the documented Rust, TypeScript, and Dart clients for `/v1/stt`, `/v1/tts`, and `/v1/translate`. The packages are intentionally thin transports: URL construction, optional bearer auth, JSON encoding/decoding, and typed error-envelope mapping. They do not retry, cache, stream, or add business logic. Optional fields are omitted rather than serialized as null, non-2xx responses become typed errors, and long audio remains request/response under the current 25 MB cap.

No private source content is embedded beyond the documented public-facing usage contract.

## Publish

1. Create public repository `voxletra.github.io` in the `voxletra` organization.
2. Copy this directory to the new repository root.
3. Run `npm install && npm run build`.
4. Add the standard Astro GitHub Pages workflow and enable GitHub Actions as the Pages source.
5. Verify `https://voxletra.github.io/` and update the linked GitHub and Linear tickets.
