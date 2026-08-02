# DocuFlow Releases

Repositorio publico para distribuir instaladores oficiales de DocuFlow.

Este repositorio no contiene el codigo fuente de DocuFlow. Su objetivo es publicar binarios instalables mediante GitHub Releases, para que la pagina de SanoTecno pueda ofrecer descargas directas sin ocupar espacio en el servidor de aplicaciones.

## Descargas

Cuando exista una release publicada, los enlaces estables quedaran asi:

- macOS Apple Silicon: `https://github.com/sanotecnologias/docuflow-releases/releases/latest/download/DocuFlow-0.1.0-mac-arm64.dmg`
- Windows x64: `https://github.com/sanotecnologias/docuflow-releases/releases/latest/download/DocuFlow-0.1.0-win-x64.exe`

## Archivos actuales

Los instaladores generados actualmente estan en:

- `/Users/tony/Documents/Generador de documentacion/release/DocuFlow-0.1.0-mac-arm64.dmg`
- `/Users/tony/Documents/Generador de documentacion/release/DocuFlow-0.1.0-win-x64.exe`

## Flujo de publicacion

1. Generar instaladores desde el repositorio privado de DocuFlow.
2. Crear una release en este repositorio con la version correspondiente.
3. Adjuntar los instaladores como assets de la release.
4. Usar los enlaces de GitHub Releases en la pagina de SanoTecno.

## Reglas

- No subir codigo fuente.
- No versionar instaladores dentro del historial de git.
- No subir llaves, tokens, archivos `.env` ni credenciales.
- Publicar instaladores solo como assets de GitHub Releases.
