# Dataset

## Class definitions

| ID | Class | Meaning | Label it when |
|---|---|---|---|
| 0 | `person` | A visible human | Most of the body or at least head and shoulders are visible |
| 1 | `helmet` | A safety helmet (hard hat) worn on a head | The helmet is on someone's head. Do not label helmets lying on tables or held in hands |
| 2 | `no_helmet` | A head with no safety helmet | The head is clearly visible and uncovered, or covered by a normal cap, hood or hair only |

Box the **head area only** for `helmet` and `no_helmet` (top of helmet to chin), and the whole visible body for `person`. If you cannot tell whether a head has a helmet (too small, blurred, hidden), leave it unlabelled. The app shows such people as **Unknown**.

The app also accepts other class names. `config.yaml` maps names such as `Hardhat`, `NO-Hardhat` and `head` onto these three meanings, so public datasets can be used without renaming.

## Design choice

The app can use direct `no_helmet` visual evidence. By default, it also treats a confidently detected person with no associated helmet evidence as No Helmet (`derive_no_helmet: true`). This supports models trained without a `no_helmet` class, but can produce false alerts when a head is hidden or the helmet is missed. Set `derive_no_helmet: false` in `config.yaml` to require direct `no_helmet` evidence instead.

## Folder layout

```
datasets/
├── data.yaml
├── images/
│   ├── train/   (about 70%)
│   ├── val/     (about 20%)
│   └── test/    (about 10%, never used for training or tuning)
└── labels/
    ├── train/   one .txt per image, YOLO format: class x_center y_center width height (0-1)
    ├── val/
    └── test/
```

## Getting data

- **Public datasets:** search Roboflow Universe or Kaggle for "hard hat detection" or "safety helmet detection", and export in **YOLOv8 / YOLO11** format. Check the licence before using it.
- **Your own images:** take photos or extract video frames from the real camera position, then label them with a tool such as Label Studio, CVAT or Roboflow.

To keep results reliable:
- **Variety:** include different helmet colours, indoor and outdoor scenes, low light, strong backlight, near and far people, several camera angles, and partly hidden heads.
- **Avoid leakage:** frames from the same video clip must all stay in one split. Never put near-duplicate frames in both train and test.
- **Record what you used:** the source, licence, image count per split and per class, and any cleaning you did. Add these to the table below.

| Item | Value |
|---|---|
| Source(s) | |
| Licence | |
| Images (train / val / test) | |
| Labels per class | |
| Environments covered | |
