# docker-geckodriver

Includes

* GeckoDriver (Latest)
* Firefox (Latest Stable)

## Building the Docker Image

You can build the image by either building from GitHub or cloning the repository.

```
docker build -t docker-geckodriver:latest .
```

## Usage

The most basic usage is to run the container and expose the ChromeDriver port on all interfaces.

```
docker run --name geckodriver -P -d docker-geckodriver:latest
```

If you want to restrict the ports to your local environment, you can do so using `-p`.

```
docker run --name geckodriver -p 127.0.0.1::4444 docker-geckodriver:latest
```

***Note:*** ChromeDriver restricts access to local connections by default.  To allow external connections, you can pass in a custom `CHROMEDRIVER_WHITELISTED_IPS` environment variable.  By default, this is set to `127.0.0.1`, but this can be any comma separated list of IP addresses.  Setting the value as empty will allow all remote connections.

```
docker run --name geckodriver -p 127.0.0.1::4444 -e CHROMEDRIVER_WHITELISTED_IPS='' docker-geckodriver:latest
```

### Environment variables

| Variable      | Description   | Default |
| ------------- |---------------| ---------|
| `CHROMEDRIVER_WHITELISTED_IPS` | list if comma separated IPs or `''` to allow all | 127.0.0.1 |
| `CHROMEDRIVER_VERBOSE` | `--verbose` to run geckodriver in verbose mode | empty |
| `CHROMEDRIVER_PORT` | port number to run geckodriver on | 4444 |
| `SCREEN_GEOMETRY` | screen resolution settings for `Xvfb` | `"1440x900x24"` |


### Verbose Logging

You need to pass `--priviledged=true` otherwise Chrome won't start

```sh
$ docker run --name geckodriver -P -d -e CHROMEDRIVER_WHITELISTED_IPS='' -e CHROMEDRIVER_VERBOSE='--verbose' --privileged=true geckodriver:latest
 ```

### Viewing the Logs

Chromedriver logs can be found in `/var/log/supervisor/geckodriver.log`