# Image Metadata Editor

[Español](README.md) · **English**

[![CI](https://github.com/Serberar/editor-metadatos-imagenes/actions/workflows/ci.yml/badge.svg)](https://github.com/Serberar/editor-metadatos-imagenes/actions/workflows/ci.yml) [![Version](https://img.shields.io/github/v/release/Serberar/editor-metadatos-imagenes?label=version)](https://github.com/Serberar/editor-metadatos-imagenes/releases/latest)

Windows desktop app (Python and Tkinter) that reads, edits and adds image metadata, and copies a field (for example `Comment`) from one image to many others in one go.

The interface is in Spanish.

## What it does

- Shows all metadata: format, size, EXIF, GPS, PNG text fields and the raw list of PNG chunks (including the ones Pillow ignores, such as C2PA `caBX` signatures).
- Edits, adds and deletes fields:
  - **PNG**: text fields with any name (`Comment`, `prompt`, `Author`...).
  - **JPEG**: `Comment` (COM marker) and standard EXIF tags (`Artist`, `Copyright`, `ImageDescription`, `Software`, `DateTime`...).
  - **TIFF / WEBP**: standard EXIF tags.
- Copies a field to many images at once, overwriting the originals or creating `<name>_editado` copies.
- Saves to a new file by default and warns about unsaved changes.

## Download

**[Download editor_metadatos.exe](https://github.com/Serberar/editor-metadatos-imagenes/releases/latest/download/editor_metadatos.exe)** (Windows, no Python needed).

Windows may show a SmartScreen warning because the executable is not signed: click *More info* > *Run anyway*.

## Run from source

Requires Python 3.10 or later and [Pillow](https://pypi.org/project/pillow/):

```bash
pip install -r requirements.txt
python editor.py [image]
```

Read metadata from the console only:

```bash
python metadata.py image1.png image2.jpg
```

## Copy `Comment` to other images

1. Open the image that has the field.
2. Select the field in the table (if none is selected, `Comment` is used).
3. Click **Copiar campo a otras imagenes...** and pick the targets.
4. Choose whether to overwrite the originals or create `_editado` copies.

## Build the executable

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --name editor_metadatos editor.py
```

The executable ends up in `dist/editor_metadatos.exe`. Open it with a double click or by dropping an image on it.

## Tests

```bash
python test_editor.py
```

## Limitations

- Saving a JPEG recompresses it (with the same quantization tables, so the loss is minimal).
- Saving a PNG drops the chunks Pillow does not recognize.
- It does not edit GPS or camera data in EXIF.
- Copying a hash or signature (such as `ci1:...`) to another image does not make it valid for that image.

## License

Released under the [MIT](LICENSE) license.

## Author

Sergio Bernabé
