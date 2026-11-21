# Changelog

All notable changes to `qalainau/filament-warp-clipboard` are documented here.

## [1.0.0] - 2026-11-21

### Added

- `WarpClipboardPlugin` remembers copies made in a Filament panel: Ctrl+C / ⌘C, the browser's Copy command, Filament `copyable()` and any `navigator.clipboard.writeText()` call.
- The last 10 distinct copies (`limit()`), with where each was copied (row and column, entry or field label, or page heading) and how long ago.
- Keep items you reuse, and add your own named text; kept items survive closing the browser unless `persist(false)`.
- A paste picker in text fields: Ctrl+Shift+V / ⌘⇧V at the caret, or right-click when the history is not empty. Shift + right-click keeps the browser menu. Pasting updates Livewire and Alpine bindings.
- A clipboard button in the top bar (`topbarButton(false)` hides it) to copy again, keep, edit, remove and add text.
- Password, one-time-code, new-password and current-password fields, and anything inside `data-warp-no-clipboard`, are never remembered.
- History is stored only in the browser, separately per panel, user and tenant.
- Search, keyboard navigation, a bottom sheet on phones, light and dark mode, RTL and ten languages.
- Works on its own; with Warp Context Menu installed, its menus gain a Clipboard submenu (`window.WarpClipboard`).
