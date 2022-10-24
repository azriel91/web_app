# Deploying

<!-- https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6 -->

These instructions set up `web_app` to run on an Ubuntu server.

1. Set up SSH configuration to authenticate with the `web_app`.

    The following assumes access to the server as the `ubuntu` user with passwordless `sudo`:

    **Note:** Make sure to replace the IP address with that of your server.

    ```bash
    # `~/.ssh/config`
    Host web_app_host
      HostName 127.0.0.1 # Replace this with the server's IP
      User ubuntu
      IdentityFile ~/.ssh/your_private_key
    ```

2. Copy across the session server binary and accompanying files.

    ```bash
    scp ./web_app         web_app_host:/home/ubuntu
    scp ./web_app.service web_app_host:/home/ubuntu
    ```

3. Log into the server, and set up the `web_app` service.

    ```bash
    # Log in
    ssh web_app_host
    ```

    Then:

    ```bash
    sudo mv /home/ubuntu/web_app.service /etc/systemd/system/
    sudo systemctl start web_app
    sudo systemctl enable web_app
    ```
