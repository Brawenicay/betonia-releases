# Per-client update channels

Each file here is a release manifest for exactly one customized client build —
`latest-<channel>.json`, same shape as the root `latest.json`:

```json
{
  "version": "1.0.0",
  "url": "https://github.com/Brawenicay/betonia-releases/releases/download/<tag>/<installer>.exe"
}
```

A client's app only reads this file if it was built from that client's own Git branch
(where `UpdateChannel.Current` in `StockManager.Domain/Common/UpdateChannel.cs` was set to
`<channel>` instead of `"default"`). Regular clients never touch this folder — they read
the shared `latest.json` at the repo root, same as always.

Publishing a new version for one client means updating **only their own**
`latest-<channel>.json` — never the root `latest.json`, and never another client's file.
That's what keeps one client's update from ever reaching anyone else.

See `CLIENTS.md` in the main app repo for the registry of which channel/branch belongs to
which client.
