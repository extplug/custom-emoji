Custom Emoji
============

ExtPlug plugin that allows room owners to specify custom emoji.
:awesome:

## Installation

If you do not have ExtPlug yet, get it [here](https://extplug.github.io).

You can install this plugin by going to your ExtPlug settings menu, pressing
"Install Plugin", and entering this Plugin URL:

```
https://unpkg.com/extplug-custom-emoji
```

## Room Settings

**Note: This section is intended for room hosts only.**

You can add custom emoji to your room by adding an `emotes` property to
your room settings file. The `emotes` property should contain an object,
with emoji names as keys, and emoji images as values.

> You can also use the `emoji` property, but then your custom emoji
> won't work for users of the Radiant Community Script.

An emoji image can be:

  * a URL string. This will use the image at the given URL as the emoji.
    This is the simplest method and is *probably* what you should use,
    unless you have hundreds of emoji.
    (eg. `{ "my_emoji": "https://example.com/my_emoji.png" }`)
  * a Sheet object. This will use a sprite sheet at a given URL, and
    grab the emoji from that. You have to specify both the URL, and the
    offset at which your emoji can be found. The `x` and `y` offset
    properties form the value for a CSS `background-position` property,
    so they should usually be negative and include the `px` suffix.

    For example, an emoji at 75px from the left, and 300px from the top,
    in image sheet `sprite_sheet.png` needs the following JSON:
    ```json
    "my_emoji": {
      "sheet": "https://example.com/sprite_sheet.png",
      "x": "-75px",
      "y": "-300px"
    }
    ```
    Using a sprite sheet means you can load lots of emoji in one go,
    instead of waiting for dozens of small images to download, so it may
    be faster.
  * a Style object. This will apply any CSS styles you enter to the
    emoji.
    For example:

    ```json
    "pink_square": {
      "background": "magenta",
      "border": "1px solid lime"
    }
    ```

Individual emoji should be exactly 15px by 15px in size. If they are
smaller (or larger), they will be scaled to fit in a 15px by 15px box.

Full example:

```json
{
  "emotes": {
    "smiling_bunny": "https://example.com/smiling_bunny.png",
    "sad_bunny_one": {
      "sheet": "https://example.com/sad_bunnies.png",
      "x": "-15px",
      "y": "0px"
    },
    "sad_bunny_two": {
      "sheet": "https://example.com/sad_bunnies.png",
      "x": "-15px",
      "y": "-15px"
    }
  }
}
```

Now, users can use the `:smiling_bunny:`, `:sad_bunny_one:`, and
`:sad_bunny_two:` emoji.

## Building

**Note: this section is intended for developers only.**

First, install dependencies:

```bash
npm install
```

Then, use:

```bash
npm run build
```

The plugin will be built using the [ExtPlug CLI](https://github.com/extplug/extplug-cli).

The built plugin will be stored at `build/custom-emoji.js`.

## License

[MIT](./LICENSE)
