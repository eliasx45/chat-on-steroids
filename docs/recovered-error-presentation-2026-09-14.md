# Recovered interruption presentation — 2026-09-14

## Bottom line

ChatGPT can finish an answer on the server after its page displays `Connection interrupted` and
Chat On Steroids reloads the page. Reload loses the document-local turn id, so the recorder may
retain several honest error occurrences while the stable final is stored without that old id.
The desktop previously left every occurrence as a red active warning even after the recorder had
independently proved the stable final belonged to the uncertain response.

The renderer now uses that existing `goalEligible` final proof to present the affected error cards
as recovered. The proof is bounded by the next authored user message; unrelated later answers do
not rewrite an older failure. Recording and browser-repair authority are unchanged.

## Evidence

- Installed app: 2.1.11 on macOS.
- Live signed-in ChatGPT conversation and its matching local session were inspected without
  publishing their identifiers or authored content.
- The durable journal recorded recoverable errors at sequences 27, 31 and 36, browser repairs at
  28/29 and 37/38, and the stable final at sequence 40 with `goalEligible: true`.
- Live ChatGPT showed the final plan and later tool work; the old provider error banner was gone.

## Validation

- `npm test -- --run test/chat-error-presentation.test.ts`
- `npm test -- --run test/renderer-timeline.test.ts test/renderer-i18n.test.ts test/renderer-recovery.test.ts test/session.test.ts`
- `npm run typecheck`
- `npm run build`
- `npm run verify` ran 4,383 tests: 4,253 passed, 129 skipped, and one unchanged
  code-mode CPU-budget timing assertion failed under the full parallel load. Its isolated rerun,
  `npm test -- --run test/code-mode-runtime.test.ts`, passed all 14 tests.
- `npm run dist:dir:mac:arm64`; the resulting app passed strict deep `codesign` verification.

Installed-package and live desktop verification are recorded in the delivery report after packaging.
