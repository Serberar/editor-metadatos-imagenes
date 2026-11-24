# Editor de metadatos de imágenes

**Español** · [English](README.en.md)

[![Versión](https://img.shields.io/github/v/release/Serberar/editor-metadatos-imagenes?label=versi%C3%B3n)](https://github.com/Serberar/editor-metadatos-imagenes/releases/latest)

Programa de escritorio para Windows (Python y Tkinter) que lee, edita y añade metadatos de imágenes, y copia un campo (por ejemplo `Comment`) de una imagen a muchas otras de una vez.

## Qué hace

- Muestra todos los metadatos: formato, tamaño, EXIF, GPS, campos de texto PNG y la lista de chunks PNG en crudo (incluidos los que Pillow ignora, como firmas C2PA `caBX`).
- Edita, añade y borra campos:
  - **PNG**: campos de texto con cualquier nombre (`Comment`, `prompt`, `Autor`...).
  - **JPEG**: `Comment` (marcador COM) y etiquetas EXIF estándar (`Artist`, `Copyright`, `ImageDescription`, `Software`, `DateTime`...).
  - **TIFF / WEBP**: etiquetas EXIF estándar.
- Copia un campo a varias imágenes en lote, sobrescribiendo los originales o creando copias `<nombre>_editado`.
- Guarda por defecto en un archivo nuevo y avisa si hay cambios sin guardar.

## Descarga

**[Descargar editor_metadatos.exe](https://github.com/Serberar/editor-metadatos-imagenes/releases/latest/download/editor_metadatos.exe)** (Windows, no necesita Python).

Windows puede mostrar un aviso de SmartScreen porque el ejecutable no está firmado: pulsa *Más información* > *Ejecutar de todas formas*.

## Ejecutar desde el código

Requiere Python 3.10 o superior y [Pillow](https://pypi.org/project/pillow/):

```bash
pip install -r requirements.txt
python editor.py [imagen]
```

Solo leer metadatos desde la consola:

```bash
python metadata.py imagen1.png imagen2.jpg
```

## Copiar `Comment` a otras imágenes

1. Abre la imagen que tiene el campo.
2. Selecciona el campo en la tabla (si no seleccionas ninguno se usa `Comment`).
3. Pulsa **Copiar campo a otras imagenes...** y elige los destinos.
4. Elige si sobrescribir los originales o crear copias `_editado`.

## Crear el ejecutable

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --name editor_metadatos editor.py
```

El ejecutable queda en `dist/editor_metadatos.exe`. Se abre con doble clic o arrastrando una imagen encima.

## Pruebas

```bash
python test_editor.py
```

## Limitaciones

- Guardar un JPEG lo recomprime (con las mismas tablas de cuantización, la pérdida es mínima).
- Al guardar un PNG se pierden los chunks que Pillow no reconoce.
- No edita GPS ni los datos de cámara del EXIF.
- Copiar un hash o firma (como `ci1:...`) a otra imagen no lo hace válido para esa imagen.

## Licencia

Publicado con licencia [MIT](LICENSE).

## Autor

Sergio Bernabé
