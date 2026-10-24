# Redis Core

*An educational project showcasing how to use Redis with Python, covering both synchronous and asynchronous approaches.* [^1]

[^1]: Redis offers a rich set of features (e.g. data structures, pub/sub, streams, Lua scripting). However, this project focuses on its original and most common use case: a fast, simple, and reliable cache. While Redis can do much more, here I intentionally limit the implementation to classic key-value caching to keep the example clear, educational, and aligned with Redis’s core purpose.

> [!WARNING]  
> **Project Archived**
> 
> This project is no longer actively maintained. 
> 
> **Context:**  
> Originally, this repository began as a modular component of a large-scale university assignment. Rather than simply completing the task and discarding the code, I chose to expand it into a structured mini-project to deeply explore how to work with Redis in practice. Over time, however, I decided to consolidate all the modular knowledge I gained in web technologies into a single, unified educational project. Maintaining "perfect educational code" for Redis across multiple separate repositories became inefficient and fragmented.
> 
> **Reason for Archiving:**  
> Consequently, I made the decision to archive this standalone project to consolidate and maintain the highest quality, up-to-date code in a single location. 
> 
> This repository remains available purely as an educational reference for those interested in a foundational understanding of how to work with Redis in practice. For the most up-to-date and comprehensive implementation, please refer to my main unified project:
> 
> - [Pose Estimation Service](https://github.com/snegoviol/pose-estimation-service)
> 
> Additionally, you can explore further examples of my architecture and development approach in these repositories:
> - [Backend Core](https://github.com/snegoviol/backend-core)
> - [Fullstack Core](https://github.com/snegoviol/fullstack-core)

## Project Structure

```
redis-core/
├── app/                   # Main application code
├── docker-composes/       # Docker Compose configurations for Redis servers
├── .env.example           # Example environment variables file
├── justfile               # Project-specific commands using Just
├── pixi.lock              # Locked dependency versions for reproducible environments
├── pixi.toml              # Pixi project configuration: environments, dependencies, and platforms
└── playground-testing/    # Jupyter notebooks for playground testing
```

Each directory includes its own `README.md` with detailed information about its contents and usage, and every file contains comprehensive inline comments to explain the code.

## Dependencies Overview

| Dependency | Repository | What it is |
| :--- | :--- | :--- |
| **CPython** | [python/cpython](https://github.com/python/cpython) | The de facto standard implementation of the Python programming language. |
| **pydantic-settings** | [pydantic/pydantic-settings](https://github.com/pydantic/pydantic-settings) | Pydantic-powered library for managing application configuration and environment variables with strong typing, validation, and seamless `.env` support. |
| **redis-py** | [redis/redis-py](https://github.com/redis/redis-py) | The official Python client for Redis, used here for synchronous and asynchronous caching operations. [^2] |
| **just** | [casey/just](https://github.com/casey/just) | Lightweight, cross-platform command runner that replaces complex shell scripts with clean, readable recipes, and natively loads environment variables directly from `.env` files out of the box (unlike `pixi tasks`). |
| **JupyterLab** *(Dev)* | [jupyterlab/jupyterlab](https://github.com/jupyterlab/jupyterlab) | Next-generation web-based interactive development environment for Jupyter notebooks; used here to create interactive documents for testing and verifying code execution. |

[^2]: I use `redis-py` directly instead of higher-level libraries like `redis-om` because this project focuses solely on simple key-value caching, and advanced features are unnecessary for this use case.

## Quick Start

### I. Prerequisites

| Component | Requirement |
| :--- | :--- |
| **Operating System** | GNU/Linux-based system |
| **Architecture** | `x86_64` |
| **Package Manager** | [`Pixi`](https://pixi.prefix.dev/latest/) |
| **Container Tools** | [Docker and Docker Compose](https://docs.docker.com/engine/install/) |

> **Note:**  
> These are not strict requirements, but rather the baseline environment where the code is 
> guaranteed to run out of the box. Alternative setups are possible but may require manual 
> configuration.

### II. Environment Setup

1. **Clone the repository**

    ```bash
    git clone https://github.com/snegoviol/redis-core.git
    cd redis-core
    ```

2. **Install dependencies**

    ```bash
    pixi install --all
    ```

3. **Activate Pixi environment**

    ```bash
    pixi shell
    ```

4. **Setup environment configuration**

    ```bash
    just copy-env
    just make-x
    just gen-acl
    ```

5. **Start Redis database**

    ```bash
    just redis-up 2
    ```

### III. Testing

Once the database is ready, you can run and test the Redis implementation with interactive Jupyter notebooks in `playground-testing/`:

1. **Launch JupyterLab**

    ```bash
    pixi run -e test jupyter lab
    ```

2. **Test the Redis implementation**
    - JupyterLab should open automatically in your browser at the default address.
    - In JupyterLab, navigate to the `playground-testing/` folder.
    - Open and execute the notebooks interactively.

3. **(Optional) Verify database manually**  
    You can open a Redis shell to manually verify that everything is working correctly:

    ```bash
    just redis-shell 2
    ```

### IV. Cleanup

When you finish testing:

1. **Stop JupyterLab**  
    In the terminal where JupyterLab is running, press `Ctrl+C` to shut it down.

2. **Stop Redis**

    ```bash
    just redis-down 2
    ```

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).
