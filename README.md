# [VIA Web Application](https://usevia.app) - Your keyboards best friend

> **About this fork:** This fork exists to provide VIA support and EC diagnostic tools for the KBDFans Agar Mini EC. See [Agar Mini EC tools](#agar-mini-ec-tools) for setup instructions.

![android-chrome-192x192](https://user-images.githubusercontent.com/1714072/222621960-ddfb8ee6-a486-4c66-8852-b204ba7c807b.png)

VIA is a powerful, open-source web-based interface for configuring your [QMK](https://qmk.fm)-powered mechanical keyboard. It allows you to customize your keymaps, create macros, and adjust RGB settings (if it has RGB) on the fly, without needing to recompile your keyboard's firmware. This makes keyboard customization easier and more accessible for everyone.

## Agar Mini EC tools

This branch adds built-in support for the KBDFans Agar Mini EC (VID `0x9D5B`, PID `0x2509`), including regular VIA remapping and an **EC Tools** panel for adjusting EC sensitivity and viewing live per-key ADC values. The panel can help diagnose delayed or out-of-order key presses; the [full investigation and firmware-fix walkthrough](https://habr.com/ru/articles/1056772/) explains the underlying issue.

![Agar Mini EC Tools showing live per-key ADC values in VIA](https://habrastorage.org/r/w1560/getpro/habr/upload_files/9e0/934/8db/9e09348db363d322608422cd8f3a02d4.png)

### Run locally

Install [Node.js 18 or newer](https://nodejs.org/), then run:

```bash
git clone --branch dumch/local https://github.com/D00mch/app.git
cd app
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in a WebHID-capable browser such as Chrome or Edge.

### Set up the keyboard

1. Connect the Agar Mini EC over USB, click **Authorize device**, and select the keyboard. Its definition is bundled with this branch, so no JSON import is required.
2. Open **EC Tools**, press every key through its full travel, and inspect the live ADC values. Use **EC Sensitivity** to choose a suitable actuation level.
3. If fast presses are still delayed or arrive out of order and many fully pressed keys report values at or above the stock firmware's `160` cutoff, follow the firmware-patching and flashing steps in the [walkthrough](https://habr.com/ru/articles/1056772/). The EC Tools panel itself does not patch or calibrate the firmware, and the byte offset described in the article is specific to the firmware revision analyzed there.

## Getting VIA to support your keyboard

Are you a keyboard maker or a developer interested in adding support for your keyboard? We welcome contributions to the VIA project!

1. The source code of the keyboard **has to be merged** in [QMK Firmware Repositories](https://github.com/qmk/qmk_firmware) Master branch.
2. Your `keymaps/via` keymap **has to be merged** in [VIA's QMK Userspace Repository](https://github.com/the-via/qmk_userspace_via) Main branch.
3. Create a definition in JSON format for your keyboard and submit it as a pull request to [VIA's Keyboards Repository](https://github.com/the-via/keyboards) Master branch.

Please follow our [Specification documentation](https://www.caniusevia.com/docs/specification) carefully to ensure your pull request is smoothly reviewed and merged.

## Local development setup

Start by cloning [`the-via/keyboards`](github.com/the-via/keyboards) then install dependencies with `npm install` and finally `npm run build`. You should see
the output folder `dist`. This should be copied or symlinked to our repo's `public/definitions` folder.

```bash
# Inside the-via/app
public/definitions -> ../../keyboards/dist
```

### Useful commands

#### `npm run dev`

Runs the app in the development mode.
Open [http://localhost:5173](http://localhost:5173) to view it in the browser.

The page will reload if you make edits.
You will also see any lint errors in the console.

#### `npm run build`

Builds a static copy of your site to the `build/` folder.
Your app is ready to be deployed!

#### `npm run test`

Launches the application test runner.
Run with the `--watch` flag (`npm test -- --watch`) to run in interactive watch mode.

---

This project is tested with [BrowserStack](https://www.browserstack.com/).

## Looking for an offline app?

@cebby2420 has kindly made a desktop app that does so.

You can find it at [https://github.com/cebby2420/via-desktop](https://github.com/cebby2420/via-desktop).

**NOTE: This project has no official affiliation with VIA, and we cannot provide support for it.**

## Facing Issues?

If you encounter any issues or bugs while using the [VIA web application](https://usevia.app), please report them by opening an issue in the [Issues section](https://github.com/the-via/app/issues). This will help us to track down and resolve problems, and improve the VIA experience for everyone.

Before reporting, please make sure to check if an issue has already been reported. Thank you!
