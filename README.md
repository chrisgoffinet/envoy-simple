
[//]: # ( Copyright 2018 Turbine Labs, Inc.                                   )
[//]: # ( you may not use this file except in compliance with the License.    )
[//]: # ( You may obtain a copy of the License at                             )
[//]: # (                                                                     )
[//]: # (     http://www.apache.org/licenses/LICENSE-2.0                      )
[//]: # (                                                                     )
[//]: # ( Unless required by applicable law or agreed to in writing, software )
[//]: # ( distributed under the License is distributed on an "AS IS" BASIS,   )
[//]: # ( WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     )
[//]: # ( implied. See the License for the specific language governing        )
[//]: # ( permissions and limitations under the License.                      )

# envoy-simple

[![Apache 2.0](https://img.shields.io/badge/license-apache%202.0-blue.svg)](LICENSE)

Envoy-simple is a Docker image of [Envoy proxy](https://envoyproxy.github.io)
that makes it easy to configure Envoy from a dynamic control plane. Instead of
an Envoy configuration file, envoy-simple pulls all its configuration over
[Envoy's xDS APIs](https://www.envoyproxy.io/docs/envoy/latest/configuration/overview/v2_overview).
Configuring the container is as easy as setting a few environment variables:

```bash
$ docker run -d \
  -e 'ENVOY_XDS_HOST=127.0.0.1' \
  -e 'ENVOY_XDS_PORT=50000' \
  -p 9999:9999 \
  -p 80:80 \
  turbinelabs/envoy-simple:0.15.1
```

If you're looking for an an Envoy configuration server,
[Rotor](https://github.com/turbinelabs/rotor) is a fast, lightweight bridge
between your service discovery and
[Envoy](https://envoyproxy.github.io). Envoy-simple can point directly to Rotor.

## Configuration

By default, envoy-simple opens up an admin port on `0.0.0.0:9999`, and looks for an xDS
server on `127.0.0.1:50000`.

It supports the following environment variables:

- **ENVOY_BASE_ID** (default: 0): sets the base ID so that multiple envoys can
  run on the same host
- **ENVOY_NODE_ID** (default: `default-node`): sets the node ID
- **ENVOY_NODE_CLUSTER** (default: `default-cluster`): sets the node cluster
- **ENVOY_NODE_ZONE** (default: `default-zone`): sets the zone in the node locality
- **ENVOY_ADMIN_IP** (default: `0.0.0.0`): sets the admin server listener ip
- **ENVOY_ADMIN_PORT** (default: `9999`): sets the admin server listener port
- **ENVOY_ADMIN_LOG** (default: `/dev/stdout`): sets the path to the admin server logfile
- **ENVOY_XDS_HOST** (default: `127.0.0.1`): sets the xDS server hostname or IP address
- **ENVOY_XDS_PORT** (default: `50000`): sets the xDS server port
- **ENVOY_XDS_CONNECT_TIMEOUT_SECS** (default: `30`): sets the timeout to
  connect to xDS services, in seconds
- **ENVOY_XDS_REFRESH_DELAY_SECS** (default: `10`): sets the delay between calls
  refresh calls to xDS
- **ENVOY_LOG_LEVEL** (default: `info`): sets the log level to one of:
  - `trace`
  - `debug`
  - `info`
  - `warning`
  - `error`
  - `critical`
  - `off`
- **ENVOY_ARGS** (default: none): additional args for the envoy binary

Envoy logs are emitted on STDERR, and by default admin server request logging is
sent to STDOUT.

## Versioning

Please see [Versioning of Turbine Labs Open Source Projects](http://github.com/turbinelabs/developer/blob/master/README.md#versioning).

## Pull Requests

Patches accepted! Please see
[Contributing to Turbine Labs Open Source Projects](http://github.com/turbinelabs/developer/blob/master/README.md#contributing).

## Code of Conduct

All Turbine Labs open-sourced projects are released with a
[Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in our
projects you agree to abide by its terms, which will be carefully enforced.
