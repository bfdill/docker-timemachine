mbentley/timemachine
====================

docker image to run netatalk (compatible Time Machine for OS X)
based off of debian:jessie

To pull this image:
`docker pull mbentley/timemachine`

Example usage:
```
docker run -d --restart=always \
  --net=host \
  --name timemachine \
  -e PASSWORD="timemachine" \
  -e VOLUME_SIZE_LIMIT="0" \
  -e LOG_LEVEL="info" \
  -e MIMIC_MODEL="TimeCapsule6,106" \
  -v /opt/timemachine:/opt/timemachine \
  -v timemachine-logs:/var/log/supervisor \
  mbentley/timemachine:latest
```

This works best with `--net=host` so that discovery can be broadcast.  Otherwise, just expose port 548 (`-p 548:548`) and then you must manually map the drive for it to show up.

If you're using an external volume like in the example above, you will need to set the filesystem permissions on disk.  By default, the `timemachine` user is `1000:1000`.

Default credentials:
  * Username: `timemachine`
  * Password: `timemachine`

Optional variables:
  * `PASSWORD` - (default - `timemachine`) sets the password for the `timemachine` user
  * `VOLUME_SIZE_LIMIT` - (default - `0`) sets the maximum size of the time machine backup
  * `LOG_LEVEL` - (default - `info`) sets the netatalk log level
  * `MIMIC_MODEL` - (default `TimeCapsule6,106`) sets the value of time machine to mimic

Thanks for [odarriba](https://github.com/odarriba) and [arve0](https://github.com/arve0) for their examples to start from.
