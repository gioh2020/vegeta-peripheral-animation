# Urchin Peripheral Animation

![mario](./mario.gif)

![mario](./maionboard.gif)

## Usage

To use my urchin animation module as-is, first add it to your config/west.yml by adding a new entry to remotes and projects:

**If you are using your own forked/cloned module, just replace the url-base: with your forked or cloned url base**

```yml
manifest:
  remotes:
      # zmk official
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: gpeye                         #new entry
      url-base: https://github.com/GPeye  #new entry
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: mario-peripheral-animation   #new entry
      remote: gpeye                       #new entry
      revision: main                      #new entry
  self:
    path: config
```

Now simply swap out the default nice_view shield for the custom one in your build.yaml file.

```yml
---
include:
  - board: nice_nano_v2
    shield: urchin_left nice_view_adapter nice_view_custom_left #flag on the peripheral half
  - board: nice_nano_v2
    shield: urchin_right nice_view_adapter nice_view_custom #Vegeta on the central half
```

## Two shields

This module ships two shields:

- `nice_view_custom` — the central half. Shows the Vegeta animation plus battery, BLE profile/pairing status and the active layer name.
- `nice_view_custom_left` — the peripheral half. Shows a waving One Piece Jolly Roger flag plus battery and this half's BLE link status to the central half (it has no visibility into the active layer or output profile, since that's central-only state in ZMK).

Use whichever one matches the role each half of your keyboard actually builds as (`ZMK_SPLIT_ROLE_CENTRAL`), not necessarily the physical left/right naming from your own `build.yaml`.