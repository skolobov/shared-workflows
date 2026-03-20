# shared-workflows

Reusable GitHub Actions composite actions for C++ CI/CD pipelines with
Conan 2 packaging.

## Actions

### `actions/conan-setup`

Sets up Python, installs Conan from `requirements.txt`, detects a Conan
profile, and optionally caches `~/.conan2`.

#### Inputs

| Input | Required | Default | Description |
| --------------------- | -------- | ----------------------------- | ------------------------------------------- |
| `python-version-file` | No | `.tool-versions` | File containing the Python version |
| `cache-conan` | No | `true` | Whether to cache `~/.conan2` |
| `cache-key-files` | No | `conanfile.py requirements.txt`| Files to hash for the cache key |

#### Usage

```yaml
- uses: actions/checkout@v6
- uses: skolobov/shared-workflows/actions/conan-setup@v1
```

### `actions/conan-remote`

Configures and authenticates a Conan remote. The remote URL is constructed
as `<remote-url>/<remote-name>`.

#### Inputs

| Input | Required | Description |
| -------------- | -------- | -------------------------------------------- |
| `remote-name` | Yes | Name of the Conan remote (e.g., `conan-rc`) |
| `remote-url` | Yes | Base URL (without the remote name suffix) |
| `remote-user` | Yes | Username for authentication |
| `remote-token` | Yes | Token or password for authentication |

#### Usage

```yaml
- uses: skolobov/shared-workflows/actions/conan-remote@v1
  with:
    remote-name: conan-stable
    remote-url: ${{ secrets.JFROG_URL }}
    remote-user: ${{ secrets.JFROG_USER }}
    remote-token: ${{ secrets.JFROG_TOKEN }}
```

## License

[MIT](LICENSE)
