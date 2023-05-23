# Web App

[![CI](https://github.com/azriel91/web_app/workflows/CI/badge.svg)](https://github.com/azriel91/web_app/actions?query=workflow%3ACI) [![codecov](https://codecov.io/gh/azriel91/web_app/branch/main/graph/badge.svg)](https://codecov.io/gh/azriel91/web_app)

Web application with hello world, health, and metadata endpoints.

The server binds to `127.0.0.1:8000` when run:

```bash
cargo run
```

The following shows the output when accessing the available endpoints:

* "Hello World" endpoint:

    ```bash
    # Web client
    $ curl http://127.0.0.1:8000/
    Hello World
    ```

* Health endpoint:

    Depending on the value in `health.txt`, the server returns a different health status.

    ```bash
    # Client requests
    for health in ok degraded down unknown invalid
    do
        echo $health > ./web_app/health.txt
        curl http://127.0.0.1:8000/health -w "\n%{http_code} " -s | tac
    done

    200 Ok
    200 Degraded
    503 Down
    503 Unknown
    503 Unknown
    ```

* Metadata endpoint:

    ```bash
    $ curl http://127.0.0.1:8000/metadata -s
    {"version":"0.1.2","description":"Web application with hello world, health, and metadata endpoints","last_commit_sha":"db4be35ece5a6805254ac853c2372eed40384e63"}
    ```

    Formatted:

    ```json
    {
      "version": "0.1.2",
      "description": "Web application with hello world, health, and metadata endpoints",
      "last_commit_sha": "db4be35ece5a6805254ac853c2372eed40384e63"
    }
    ```

### Contributing

For development instructions, please see the [contribution guide].


### Deploying

To deploy the `web_app`, please see the [deployment guide].


[contribution guide]: CONTRIBUTING.md
[deployment guide]: DEPLOYING.md
