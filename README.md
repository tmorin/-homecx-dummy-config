# homecx-dummy-cfg

> A ready-to-fork repository to host custom configuration related to [homecx].

The repository contains one [laminar] job: `update-configuration` ([update-configuration.run]).
The purpose of the job is to cleans and fetches the repository `/data/cfg`.

A [webhook] is also configured in [webhook.json] to execute the `update-configuration` job.

The following command starts `homecx` initializing it with this current GIT repository.
The SSH keys are required to be ble to clone it from SSH.

```bash
docker run \
    -p 9000:9000 \
    -p 9001:9001 \
    -v $(pwd)/bob-rsa-key:/data/.ssh/id_rsa:ro \
    -v $(pwd)/bob-rsa-key-pub:/data/.ssh/id_rsa.pub:ro \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --env HOMECX_REPOSITORY=git@github.com:tmorin/homecx-dummy-config.git \
    thibaultmorin/homecx
```

The GIT repository can also be cloned from HTTPS.
In this case, the SSH keys are longer required.

```bash
docker run \
    -p 9000:9000 \
    -p 9001:9001 \
    -v /var/run/docker.sock:/var/run/docker.sock \
    --env HOMECX_REPOSITORY=https://github.com/tmorin/homecx-dummy-config.git \
    thibaultmorin/homecx
```


[homecx]: https://github.com/tmorin/homecx
[laminar]: https://laminar.ohwg.net
[webhook]: https://github.com/adnanh/webhook
[update-configuration.run]: jobs/update-configuration.run
[webhook.json]: webhook.json