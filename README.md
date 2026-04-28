[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

# Browsey
Automate repetitive web tasks right from your own Chrome profile.

Browsey is a Chrome extension that drives your existing browser to perform routine actions for you. Use the dedicated Social Mode for hands-off social media workflows (e.g., engagement farming on [twitter](https://x.com)), or switch to General Mode for everyday automation across the web.

Here is a video of me using the web agent in social media mode. I've tasked the web agent with continuously scrolling on X and engaging with certain posts in a particular way. Don't mind the (shitty) background music.

<p align="center">
  <a href="https://youtube.com/shorts/6Acvm_3iD4k" target="_blank" rel="noopener noreferrer">
    <img src="https://img.youtube.com/vi/6Acvm_3iD4k/hqdefault.jpg" alt="YouTube video thumbnail" />
  </a>
</p>

Keep in mind: the entire website DOM is being processed and cut down tremendously before each LLM call. The web agent takes less than a second to process and decide which action to perform, which is a non-trivial task given the sheer size of the DOM for a website like x.com. In the video the agent is responsible for continuously scrolling and only interacting (in a human fashion) with valid candidate posts, achieved via a simple prompt.


## Backend

Dependencies for the backend are managed with `uv` and the `backend/pyproject.toml` file.

### Installing Dependencies

Set up the virtual environment and install dependencies:

```bash
cd backend
uv venv                   
source .venv/bin/activate 
uv sync                   
deactivate               
```

### Adding a New Dependency

To add a new dependency:

1.  Open `backend/pyproject.toml`.
2.  Add the new package to the `dependencies` list. For example, to add `requests`:
    ```toml
    # ...
    dependencies = [
        "fastapi[all]",
        "uvicorn",
        "requests"
    ]
    # ...
    ```
3.  Install the new dependency by running `uv sync` again:
    ```bash
    uv sync
    ```

    Alternatively, let `uv` handle both the install **and** the `pyproject.toml` update in one step (example):
    ```bash
    uv add requests
    ```

### Starting the Server

Before running the server (especially after a `git pull`), update dependencies inside the venv:

```bash
source .venv/bin/activate
uv sync
deactivate
```

Then start the backend server from the backend directory:

```bash
./run.sh
```

## Extension

To start the Chrome extension development server, run the following commands from the root directory in a new terminal window:

```bash
cd extension
npm install
npm run dev
``` 
