# N.O.V.A. — Entorno Local de IA para Desarrollo

Configuración base con **Docker**, **Ollama** y **Open WebUI** para ejecutar nuestro asistente de programación de forma local (C#, PHP y frontend).

## Requisitos previos

* **Docker Desktop** instalado y en ejecución.
* **Visual Studio Code** con la extensión **Continue** instalada.

---

## Paso 1: Clonar el repositorio

Descarga este proyecto en tu computadora y entra a la carpeta:

    git clone https://github.com/Hilariordz/N.O.V.A.git
    cd N.O.V.A

---

## Paso 2: Levantar los contenedores

Inicia Ollama y Open WebUI en segundo plano:

    docker compose up -d

Verifica que ambos contenedores estén activos (`nova-ollama` y `nova-webui`):

    docker compose ps

---

## Paso 3: Descargar los modelos de IA

Descarga los dos modelos dentro del contenedor de Ollama (solo se hace la primera vez):

    docker exec -it nova-ollama ollama pull gemma3:4b
    docker exec -it nova-ollama ollama pull qwen2.5-coder:1.5b

---

## Paso 4: Entrar al chat web (Open WebUI)

1. Abre tu navegador y entra a `http://localhost:3000`.
2. Crea tu usuario local 
3. Selecciona el modelo **gemma3:4b** para consultas, arquitectura y revisión de código.

---

## Paso 5: Configurar Continue en VS Code

1. Abre VS Code y abre el archivo de configuración de Continue (`~/.continue/config.yaml`).
2. Pega la siguiente configuración y guarda el archivo:

    name: NOVA Local Config
    version: 0.0.1
    schema: v1

    models:
      - name: NOVA Chat (Gemma 3 4B)
        provider: ollama
        model: gemma3:4b
        apiBase: http://localhost:11434
        roles:
          - chat
          - edit
          - apply

      - name: NOVA Autocomplete (Qwen 2.5 Coder 1.5B)
        provider: ollama
        model: qwen2.5-coder:1.5b
        apiBase: http://localhost:11434
        roles:
          - autocomplete

---

## Comandos útiles del día a día

* **Ver contenedores activos:** `docker compose ps`
* **Apagar todo al terminar el día (sin borrar datos):** `docker compose stop`
* **Volver a encender:** `docker compose up -d`