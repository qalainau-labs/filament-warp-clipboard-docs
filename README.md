# Warp Clipboard

Clipboard history for Filament v5 panels. Keep the last copies, pin text you reuse, and paste into a field from a searchable list. Works on desktop and in a bottom sheet on smaller screens, with dark mode and RTL support.

[![Try the live demo](art/live-demo.png)](https://demo.warpui.com/clipboard)

## Installation

> **Warp Clipboard is a commercial plugin.** A license is required. After purchase you receive credentials for the private Composer repository.

```bash
composer config repositories.qalainau composer https://qalainau.privato.pub/composer
composer config --auth http-basic.qalainau.privato.pub "your-email" "your-license-key"
composer require qalainau/filament-warp-clipboard
php artisan filament:assets
```

No migrations are needed. Register the plugin on each panel:

```php
use Qalainau\FilamentWarpClipboard\WarpClipboardPlugin;

$panel->plugin(WarpClipboardPlugin::make());
```

Run `php artisan filament:assets` again after updating.

### AI coding assistants (Laravel Boost)

Warp Clipboard includes Laravel Boost guidelines and the `warp-clipboard-development` skill. Run `php artisan boost:update` after installing or updating the plugin so your coding assistant receives the current API and usage guidance.

## Configuration

```php
WarpClipboardPlugin::make()
    ->limit(10)
    ->persist(true)
    ->topbarButton(true);
```

- `limit(int $limit)`: how many recent copies to retain. `0` retains only kept text.
- `persist(bool $persist = true)`: retain kept text across browser sessions. Set `false` to keep it only in the current tab.
- `topbarButton(bool $condition = true)`: show the clipboard icon in the panel topbar.

The plugin ID is `warp-clipboard`. It activates only on authenticated panel pages.

## Usage

Copy text normally, including Filament copyable values. In an editable text field, press **Ctrl+Shift+V** (Mac: **⌘⇧V**) to open the picker at the caret. Search by name or text, then click an entry or press Enter to replace the selected range and notify Livewire of the change. Right-click opens the picker when history has entries; Shift + right-click opens the browser menu.

Use the clipboard icon in the topbar to open the manager. Each entry offers **Copy again**, **Keep / Stop keeping**, **Edit** (kept text only), and **Remove**. **Remove all** clears recent copies; when kept text exists the action becomes **Remove all except kept items**.

Choose **＋ Add text** to create kept text with an optional name. The editor accepts nonblank text up to 5,000 characters. Kept entries appear above recent copies. Arrow keys, Home, End and Escape work throughout the lists; Escape clears a search first, then closes and restores focus.

## Fields excluded from history

Passwords are excluded, including Filament revealable password fields after revealing them. Fields with `autocomplete="one-time-code"`, `new-password`, or `current-password` are excluded. Opt out an entire region or a field with:

```html
<div data-warp-no-clipboard>
    <input type="text">
</div>
```

Blank copies and text longer than 5,000 characters are ignored. The picker does not open in excluded, disabled or read-only fields.

## Browser storage

Recent copies use `sessionStorage`. Kept text uses `localStorage`, or `sessionStorage` with `persist(false)`. Storage keys separate panel, user and tenant. Signing out does not erase kept text; the same user can use it again when signing back in. Clipboard history is stored in the browser and is never sent to the server.

## Warp Context Menu

Both plugins work independently. When installed together, Warp Context Menu adds a Clipboard submenu using Warp Clipboard's history and editor. To hide that submenu for a table:

```php
$table->contextMenuClipboard(false);
```

Warp Clipboard handles right-clicks in editable text fields before the Context Menu handler.

## Translations

Includes English, Japanese, German, French, Spanish, Italian, Brazilian Portuguese, Korean, Simplified Chinese and Traditional Chinese. Text uses `warp-clipboard::clipboard` and the current application locale.

```bash
php artisan vendor:publish --tag=filament-warp-clipboard-translations
```

Override strings in `lang/vendor/warp-clipboard/<locale>/clipboard.php`.

## License and support

Proprietary. See [LICENSE.md](LICENSE.md). [Get support](https://warpui.com/support?plugin=clipboard).
