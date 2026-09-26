# bqa

`bqa` es Beequa desde el terminal: el chat, y lo que tu cuenta alcanza de
tus organizaciones y workspaces, con la misma sesión que usas en la web. Este
repositorio no tiene código: publica los binarios de cada versión.

## Instalar

**Linux y macOS** (x64 y arm64; en Linux, distribuciones con glibc):

```sh
curl -fsSL https://github.com/Beequa-Labs/bqa/releases/latest/download/install.sh | sh
```

Lo deja en `~/.local/bin/bqa`. Si esa carpeta no está en tu `PATH`, el
instalador te lo dice.

**Windows** (x64 y arm64), en PowerShell:

```powershell
irm https://github.com/Beequa-Labs/bqa/releases/latest/download/install.ps1 | iex
```

Lo deja en `%LOCALAPPDATA%\Programs\bqa\bqa.exe` y añade esa carpeta al `PATH`
de tu usuario; abre una terminal nueva después.

Los dos instaladores bajan el binario de tu plataforma y el `SHA256SUMS` de
la misma versión, comprueban el checksum y no instalan nada si no casa.

**Una versión concreta**:

```sh
curl -fsSL https://github.com/Beequa-Labs/bqa/releases/latest/download/install.sh | BQA_INSTALL_VERSION=0.1.0 sh
```

```powershell
$env:BQA_INSTALL_VERSION = '0.1.0'; irm https://github.com/Beequa-Labs/bqa/releases/latest/download/install.ps1 | iex
```

`BQA_INSTALL_DIR` cambia la carpeta de destino en los dos.

## Empezar

```sh
bqa
```

Abre el chat. La primera vez escribe `/login` con tu email y contraseña de
Beequa. Todo lo demás está en los `/comandos`: teclea `/` para verlos.

`bqa --version` dice la versión y las direcciones a las que se conecta.

La sesión se guarda en `~/.config/bqa/` (o `$XDG_CONFIG_HOME/bqa/`) en Linux
y macOS, y en `%APPDATA%\bqa\` en Windows. `/logout` la revoca y la borra.

## Actualizar

Vuelve a ejecutar el instalador: instala la última versión encima de la que
tienes. `bqa` no se actualiza solo.

**Aviso de versión nueva.** Una vez al día como mucho, en segundo plano, `bqa`
pregunta a la API de GitHub cuál es la última versión publicada aquí, y si es
mayor que la tuya lo dice en la línea de estado del chat con el comando para
actualizar. Esa consulta es la única petición que `bqa` hace fuera de Beequa,
y le dice a GitHub que tu IP usa `bqa`. Para apagarla:

```sh
export BQA_NO_UPDATE_CHECK=1
```

## Staff de Beequa

El modo `/staff` sólo aparece a cuentas con rol de plataforma de staff, y
además necesita:

- [`cloudflared`](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/)
  instalado y en el `PATH`;
- estar en la política de Cloudflare Access de la consola de Beequa.

Si falta el token de Access, `bqa` dice el comando exacto que lo consigue
(`cloudflared access login …`). Un cliente no necesita nada de esto.

## Verificar a mano

Cada release trae `SHA256SUMS` con el hash de cada fichero:

```sh
sha256sum -c --ignore-missing SHA256SUMS
```

## Desinstalar

Borra el binario (`~/.local/bin/bqa` o `%LOCALAPPDATA%\Programs\bqa\`) y la
carpeta de sesión. Haz antes `/logout` si quieres revocar la sesión en el
servidor, y no sólo borrarla de tu máquina.
