# Releases de DocuFlow

Este repositorio distribuye los paquetes compilados de DocuFlow y los recursos versionados de su IA local. El codigo fuente vive en [`sanotecnologias/docuflow`](https://github.com/sanotecnologias/docuflow). Los workflows de compilacion y publicacion estan en ese repositorio.

## Canales de instaladores

| Canal | Tag alias | Ultima version verificada | Uso |
| --- | --- | --- | --- |
| Produccion | `docuflow-latest` | `v0.1.5` | Descargas publicas de `sanotecno.com` |
| Testing | `docuflow-testing-latest` | `v0.1.3-testing.25` | Descargas de `testing.sanotecno.com` |

Las releases versionadas conservan los paquetes historicos. Los aliases se actualizan con los assets del canal y mantienen nombres estables para que el sitio no tenga que cambiar el enlace en cada version.

Assets esperados por canal:

- `DocuFlow-win-x64.zip`, con instalador Windows y manual.
- `DocuFlow-mac-arm64.zip`, con DMG, desbloqueador y manual de macOS.
- `docuflow-win.json` y `docuflow-mac.json`, con version, commit de origen, tamaño y SHA-256.

En una release versionada los nombres de los ZIP incluyen la version, por ejemplo `DocuFlow-0.1.5-win-x64.zip` y `DocuFlow-0.1.5-mac-arm64.zip`. El EXE de Windows y los manuales tambien se publican como assets individuales.

## Enlaces estables

- Windows produccion: <https://github.com/sanotecnologias/docuflow-releases/releases/download/docuflow-latest/DocuFlow-win-x64.zip>
- macOS produccion: <https://github.com/sanotecnologias/docuflow-releases/releases/download/docuflow-latest/DocuFlow-mac-arm64.zip>
- Windows testing: <https://github.com/sanotecnologias/docuflow-releases/releases/download/docuflow-testing-latest/DocuFlow-win-x64.zip>
- macOS testing: <https://github.com/sanotecnologias/docuflow-releases/releases/download/docuflow-testing-latest/DocuFlow-mac-arm64.zip>

## Release de IA local

La IA se distribuye aparte de los instaladores en el tag inmutable `docuflow-ai-v1.0.0`. Contiene el manifiesto `docuflow-ai-v1.0.0.json`, el modelo `qwen2.5-1.5b-instruct-q4_k_m.gguf`, los runtimes llama.cpp para Windows x64 y macOS arm64/x64, y sus licencias. El modelo ocupa aproximadamente 1.1 GB. DocuFlow descarga los artefactos que corresponden a la plataforma, valida sus SHA-256 y conserva los archivos en los datos del usuario.

El manifiesto fija las versiones, nombres, hashes, origen upstream y licencias. Para publicar una revision del modelo o runtime se debe crear un tag nuevo y actualizar la version fijada y los hashes en el repositorio de codigo DocuFlow; no reemplazar silenciosamente el contenido de un tag que ya distribuye una aplicacion.

## Como se publican

1. Los cambios de aplicacion se integran en `desarrollo`, se promueven a `testing` y despues a `produccion`.
2. Un push a `testing` o `produccion` ejecuta el workflow `publish-docuflow-mac.yml` del repositorio de codigo. Tambien se puede lanzar manualmente seleccionando una de esas ramas.
3. El workflow calcula la version, corre pruebas y compila Windows y macOS. Publica los ZIP, manuales y metadata versionados y actualiza el alias del canal solo al completar ambos builds.
4. Testing actualiza `docuflow-testing-latest`; produccion actualiza `docuflow-latest`. Esta publicacion no despliega la pagina de SanoTecno ni el servidor de licencias.

Los assets se publican con `scripts/publish_release.py` y el secreto `DOCUFLOW_RELEASES_GITHUB_TOKEN` del repositorio de codigo. El secreto requiere acceso de escritura a este repositorio. No almacenar tokens, instaladores ni modelos grandes en el historial Git.

## Verificacion de una publicacion

1. Abrir la release versionada y el alias del canal en [GitHub Releases](https://github.com/sanotecnologias/docuflow-releases/releases).
2. Comprobar que los dos ZIP, los manuales y ambos JSON de metadata existan. Abrir los ZIP y revisar su contenido.
3. Comparar `version` y `sourceCommit` de cada metadata con el workflow y comprobar los SHA-256 de los archivos.
4. Descargar los enlaces estables y confirmar que responden correctamente. Revisar el sitio de testing o produccion por separado, porque su despliegue es otro workflow en `sanotecnologias/home-page`.
5. Para un cambio de IA, verificar tambien el manifiesto, runtimes, modelo, hashes y licencias de `docuflow-ai-v...`.

## Reglas del repositorio

- No subir codigo fuente de la aplicacion.
- No versionar instaladores, modelos, llaves, tokens, `.env` ni credenciales en Git.
- Distribuir binarios solo como assets de GitHub Releases.
- Mantener releases versionadas para trazabilidad y aliases estables por canal.
- Consultar los resultados de GitHub Actions y la metadata antes de anunciar una nueva descarga.

La release `v0.1.0` y su nota historica describen aquella version inicial; no representan el contenido actual de los canales estables.
