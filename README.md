# Documentación DERCAS

## Requisitos

- Python 3.13 o superior.
- Poetry instalado.

## Instalar dependencias

```bash
poetry install
```

## Ejecutar la documentación

```bash
poetry run mkdocs serve
```

Luego, abrir <http://127.0.0.1:8000> en el navegador.

## Generar el sitio y el PDF

```bash
poetry run mkdocs build
```

El sitio se genera en `site/` y el PDF en:

```text
site/pdf/DERCAS-Especificaciones.pdf
```
