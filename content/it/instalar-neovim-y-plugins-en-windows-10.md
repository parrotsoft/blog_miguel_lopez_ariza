---
title: "Instalar Neovim Y Plugins en Windows 10"
date: 2021-06-12T15:17:59-05:00
draft: true
tags: ["neovim","vim","windows10"]
---

!["https://pixabay.com"](/images/monitor-933392_640.jpg "https://pixabay.com/")

**Vim** es uno editor que en la actualidad se menciona mucho en canales de **Youtuber** del area de desarrollo, especialmente en la un Fork llamado **Neovim**, te comparto los pasos para instalar en **Windows 10**.

### Instalar Chocolatey
> Chocolatey es un Gestor de Paquetes para el Sistema Operativo Windows

* Ejecutamos **PowerShell** como administrador
* Ejecutamos el siguiente comando para instalar Chocolatey, este un manejador de paquetes para Windows.

   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
   ```

### Instalar Neovim

* Ejecutamos el siguiente comando:

    ```powershell
    choco install neovim
    ```

### Instalar Vim-Plug
> vim-plug es un administrador de plugins de Vim, es minimalista y de configuración rápida.

* Creamos una carpeta para almacenar la configuracion y plugins y descargamos del repositorio de github

    ```powershell
    md ~\AppData\Local\nvim\autoload
    $uri = 'https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
    (New-Object Net.WebClient).DownloadFile(
        $uri,
        $ExecutionContext.SessionState.Path.GetUnresolvedProviderPathFromPSPath("~\AppData\Local\nvim\autoload\plug.vim")
    )
    ```

### Configurar Vim-plug

* Entramos a la carpeta:
    ```
    ~\AppData\Local\nvim\
    ```

* Creamos el archivo **init.vim**
dentro de este definiremos los plugins y configuración de los mismos, incluso este seria el archivo que necesitamos para llevar nuestro plugin de una maquina a otra.

El contenido de **init.vim** debe ser la siguiente:

```vim

    "Este es el inicio del bloque de Plugins
    call plug#begin()

        "En este punto se deben definir los plugin que se desean instalar, ejemplo:
        
        Plug 'preservim/nerdtree'

    
    call plug#end()
    "Este es el fin del bloque de Plugins

    "En la parte final del archivo se agregan configuración requeridas por los plugins, ejemplo:

    autocmd VimEnter * NERDTree

```

El paso siguiente es ejecutar la instalación de los plugin, para lo cual salimos del modo editor presionando la tecla **Esc**, escribimos **:wq** para guardar y salir.

Luego ejecutamos **:PlugInstall** con este se iniciara la instalación de los plugins.

En este punto ya estamos listos para iniciar el proceso de aprendizaje y configuración de Neovim.

Espero sea de mucha utilidad.