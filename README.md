# podman-systemd-template
A template for service-ifying and auto-updating podman containers with systemd.

On a modern Fedora- or Red Hat-like system, place your service file in the `/usr/lib/systemd/system/` directory and then run `systemctl daemon-reload` to make the new service available. Enable and start your service with `systemctl enable <my-service> --now`.

Every time the service is started, the `ExecStartPre` parameters ensure that the running container is stopped and the local container image is updated based on the path and label you supply in the `Environment=CONTAINER=` parameter.

Pods needing persistent configuration files should map storage with the `-v` parameter of `podman`, and the systemd service file includes a `RequiresMountsFor` parameter to check that the filesystem is mounted before starting the service.
