# la_cocina — Fallback estático para LumixTV

Archivos cifrados (AES-128-ECB) que la app usa cuando el servidor principal no responde.

## Estructura

```
catalog.enc          ← catálogo completo de categorías y canales
ch/{id}.enc          ← detalles de cada canal (URI, DRM, headers)
ck/{id}.enc          ← ClearKey cifrada por canal
flow_token.enc       ← token Flow actual cifrado
public_key.pem       ← clave pública RSA
```

## Cómo regenerar los archivos

1. Copiar `exportar_fallback.php` al servidor (`/www/wwwroot/lumixtv.es/SCRIPTS/`)
2. Ejecutar: `php exportar_fallback.php`
3. El script genera todos los `.enc` en el mismo directorio
4. Subir los archivos generados a este repo y hacer push

## Cuándo actualizar

| Archivo | Cuándo actualizar |
|---|---|
| `catalog.enc` + `ch/*.enc` | Al agregar/modificar/borrar canales en la DB |
| `flow_token.enc` + `ch/flow_*.enc` | Cuando vence el token de Flow |
| `ck/*.enc` | Si cambian las ClearKeys |
| `public_key.pem` | Si se genera un nuevo par de claves RSA |
