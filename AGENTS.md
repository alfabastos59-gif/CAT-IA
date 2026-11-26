<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.

## What Lovable manages

Rules outside this block are the project's own. Change the pieces below in
Lovable, not by hand. With the [Lovable MCP](https://mcp.lovable.dev)
connected, `send_message` asks Lovable to do it; otherwise ask the user to
use the editor.

- **Database.** Do not add or edit `supabase/migrations/` or `drizzle/`.
  Ask Lovable to change the schema.
- **Generated files.** Do not edit a file whose header says it is automatically
  generated.
- **AI gateway.** Keep model calls on Lovable's gateway, and keep
  `LOVABLE_API_KEY` out of browser code.
- **Connectors.** Lovable provides native connectors. `list_connectors` shows
  which are enabled; `add_connector` only returns the dashboard link. When a
  connector is enabled, calls go through the connector gateway and need
  `LOVABLE_API_KEY`. When Lovable does not provide one, users can bring their
  own key and store it in Secrets.
- **Secrets.** Lovable manages them. Do not put secret values in the repo.
<!-- LOVABLE:END -->

## Avatar media
- Keep automatic voice recognition wake-word gated, abort recognition during each response, and discard stale recognition callbacks before restarting after the echo cooldown; this prevents speaker feedback from sending new questions.
- Render the avatar from an RGB/alpha-packed video through a browser canvas, with a transparent poster fallback; this preserves transparency across mobile browsers without relying on alpha-video codec support.
- Drive Fish Audio lip sync from the decoded audio clip's normalized speech envelope synced to `audio.currentTime` (with lookahead and live `AnalyserNode` band fallback), not network-request timing; browser speech uses its playback callbacks and an approximate cadence because it exposes no audio samples.

## Assistant knowledge
- Keep Mission rules in a browser-safe structured knowledge module and include its generated context in every assistant request, so numeric rules are testable and follow-up questions retain the same source of truth.
