<!-- omit in toc -->
# slidev-esp-template

This project is a template for [Slidev](https://github.com/slidevjs/slidev) presentations recommended for use at [Espressif](https://www.espressif.com/).

You can jump to:

- [History](#history)
- [Installation and configuration](#installation-and-configuration)
  - [Software dependencies](#software-dependencies)
  - [Template setup](#template-setup)
- [Usage](#usage)
- [Learn more about Slidev](#learn-more-about-slidev)
  - [Quick tips](#quick-tips)
- [Layout and appearance](#layout-and-appearance)
  - [Visual layout settings](#visual-layout-settings)
  - [Update logo](#update-logo)
- [Slide syncing](#slide-syncing)
  - [Troubleshooting](#troubleshooting)

## History

The template is based on the Slidev [Getting Started](https://sli.dev/guide/) project with the following changes:

- **Theme**: instead of `seriph`, it uses the `default` theme.
- **Addons**: it includes
  - [slidev-addon-sync](https://github.com/Smile-SA/slidev-addon-sync) -- for usage instructions, see [Slide syncing](#slide-syncing)
  - [Poll and Quiz](https://github.com/Smile-SA/slidev-component-poll) -- see a usage example in [slides.md](./slides.md#poll-and-quiz-added-in-slidev-esp-template) > *Poll and Quiz*.
- **Layout**: Espressif logo added.
- **Slide content**:
  - Replaced Slidev Getting Started title page with a usual Espressif title page
  - Changed guidelines in *Themes*
  - Added a slide *Poll and Quiz* describing this plugin


## Installation and configuration

You can use your OS native package manager to install the dependencies, however, it is recommended to use `nvm` -- Node.js version manager.

The following instructions are provided in detail, as parts of the Node.js ecosystem may not be immediately intuitive to some users. These steps have been tested on Linux only. The general approach should be similar on other operating systems with some possible adjustments.

If you run into major problems installing and configuring the dependencies, feel free to open an issue — we’ll do our best to update the instructions accordingly.

### Software dependencies

Slidev requires `Node.js`, which can be conveniently installed using [nvm](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating):

```sh
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.nvm/nvm.sh
# Install Node.js (LTS version includes npm)
nvm install --lts
# Install pnpm globally (recommended over npm for faster installs and disk efficiency)
npm install -g pnpm
```


### Template setup

To create your presentation:

1. On the GitHub repo page, click **Use this template** in the top-right corner.
    - This creates a new repo under your GitHub account with the contents of `slidev-esp-template`.
2. Clone your new repo:
    ```sh
    git clone https://github.com/YOUR_USERNAME/slidev-esp-template.git
    cd ~/path/to/slidev-esp-template/
    ```
3. Install project dependencies:
    ```sh
    pnpm install
    ```
4. (Optional but recommended) Set up your environment to use Slidev globally:
    ```sh
    # Create a global bin directory and add it to your shell's PATH
    pnpm setup
    # Restart your shell
    # Install the Slidev CLI globally
    pnpm add -g @slidev/cli
    ```
    💡 If you prefer not to install anything globally, you can run Slidev using `pnpm exec slidev`.

## Usage

To start the slide show:

- Run `slidev`
- Visit <http://localhost:3030>

Edit the [slides.md](./slides.md) to see the changes.

Examples of Espressif presentations using Slidev:

- [DevCon23 - Developing, Publishing, and Maintaining Components for ESP-IDF](https://www.youtube.com/watch?v=D86gQ4knUnc)

## Learn more about Slidev

To get started, see:

- [Syntax Guide](https://sli.dev/guide/syntax)
- [Directory Structure](https://sli.dev/custom/directory-structure)
- [User Interface](https://sli.dev/guide/ui)

This is part of extensive Slidev [documentation](https://sli.dev/).

### Quick tips

- If you use VS Code, you can install [Slidev for VS Code](https://sli.dev/features/vscode-extension.html) extension to improve your experience using Slidev.
- **Include static files**: If you have static files, such as images or diagrams, place them in the `public/` folder. You can then reference them using `src="/image.png"`. For example, to include the image `public/myimage.jpeg` on your slide, use `src="/myimage.png"`.
- **Embed external code blocks**: If you need to include code blocks, place files containing code in the `snippets/` folder. Then:
  - Mark the regions to include:
    ```ts
    // #region snippet
    ...
    // #endregion snippet
    ```
  - Include the regions:
    ```ts
    <<< @/snippets/external.ts#snippet
    ```
- **Arrange content in slides**: You can save time arranging content in your slides using preset [layouts](https://sli.dev/guide/layout) in your slide frontmatter:
  ```markdown
  ---
  layout: two-cols
  ---
   ```
- **Simplify content reuse**: If you plan to reuse certain slides or sections in other Slidev presentations, you can place this content in separate markdown files inside the `pages/` folder, for example `pages/content.md`. To include them into your main `slides.md`, use:
  ```markdown
  ---
  src: ./pages/content.md
  hide: false
  ---
  ```
  The parameter `hide` conveniently helps to show or hide the included slides.

## Layout and appearance

### Visual layout settings

- **Color scheme**: To change the color scheme, in the `slides.md` YAML frontmatter, update the parameter `colorSchema`. The default value is `light`, but you can update it to `auto` or `dark`.
- **Aspect ratio and canvas size**: To change the configuration, in the `slides.md` YAML frontmatter, update the values of `aspectRatio` and `canvasWidth`.

### Update logo

If the slides are for an event that has its own logo (for example, DevCon25), consider replacing the standard Espressif logo with the event-specific logo.

To update the logo, follow these steps:

1. Choose the logo in the `public/` folder. If your event's logo is not there, add it and consider adding it to the upstream template repo as well.
2. In the `slides.md` YAML frontmatter, find the parameter `favicon` and add the path to the new logo.
3. Preview the slides to make sure the logo is clearly visible and works well with the slide background color.


## Slide syncing

To enable slide syncing, run:

```sh
slidev --remote=<password>
```

This command will return the links for the presenter and attendees.


### Troubleshooting

If slide syncing doesn't work, make sure that:

- The dev server (`slidev --remote`) is running somewhere (usually the presenter's device).
- The presenter is using the presenter link.
- The presenter's and attendee's devices are connected to the same network.
- The device's OS does not block access to the LAN due to the use of VPN clients, etc.
