# IBM Cloud App ID Istio Adapter

[![IBM Cloud powered][img-ibmcloud-powered]][url-ibmcloud]
[![Travis][img-travis-master]][url-travis-master]
[![Coveralls][img-coveralls-master]][url-coveralls-master]
[![Codacy][img-codacy]][url-codacy]

[![GithubWatch][img-github-watchers]][url-github-watchers]
[![GithubStars][img-github-stars]][url-github-stars]
[![GithubForks][img-github-forks]][url-github-forks]

### Summary

### Requirements

- Kubernetes Cluster
- Istio
- Helm

### Installation

The adapter can be installed using the accompanying helm chart. The chart comes with an opinionated 
set of configuration values that may be updated depending on project need.

Once your chart is configured, you will need to install `helm` followed by the adapter chart using the commands below:

```
helm init
helm install ./helm/ibmcloudappid --name ibmcloudappid
```

### Cleanup

```
helm delete --purge ibmcloudappid
kubectl delete rule ibmcloudappid-keys -n istio-system
```

### Logging

By default, the adapter logs at an INFO visibility level with a JSON styled output for ease of integration with logging systems.

**Note:** If viewing JSON logs manually you may want to tail the logs and pretty print them using [jq](https://brewinstall.org/install-jq-on-mac-with-brew/)

#### Configuration

You can update this configuration in the helm chart. Supported log levels range from [-1, 7] following the model of zapcore. See the [docs](https://godoc.org/go.uber.org/zap/zapcore#Level) for level details.

#### Adapter

```
kubectl -n istio-system logs -f $(kubectl -n istio-system get pods -lapp=ibmcloudappid -o jsonpath='{.items[0].metadata.name}')
```

#### Mixer

```
kubectl -n istio-system logs -f $(kubectl -n istio-system get pods -lapp=telemetry -o jsonpath='{.items[0].metadata.name}') -c mixer
```

### License
This package contains code licensed under the Apache License, Version 2.0 (the "License"). You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 and may also view the License in the LICENSE file within this package.

[img-ibmcloud-powered]: https://img.shields.io/badge/ibm%20cloud-powered-blue.svg
[url-ibmcloud]: https://www.ibm.com/cloud/
[img-license]: https://img.shields.io/npm/l/ibmcloud-appid.svg
[img-version]: https://img.shields.io/npm/v/ibmcloud-appid.svg

[img-github-watchers]: https://img.shields.io/github/watchers/ibm-cloud-security/appid-serversdk-nodejs.svg?style=social&label=Watch
[url-github-watchers]: https://github.com/ibm-cloud-security/appid-serversdk-nodejs/watchers
[img-github-stars]: https://img.shields.io/github/stars/ibm-cloud-security/appid-serversdk-nodejs.svg?style=social&label=Star
[url-github-stars]: https://github.com/ibm-cloud-security/appid-serversdk-nodejs/stargazers
[img-github-forks]: https://img.shields.io/github/forks/ibm-cloud-security/appid-serversdk-nodejs.svg?style=social&label=Fork
[url-github-forks]: https://github.com/ibm-cloud-security/appid-serversdk-nodejs/network

[img-travis-master]: https://travis-ci.org/ibm-cloud-security/policy-enforcer-mixer-adapter.svg?branch=master
[url-travis-master]: https://travis-ci.org/ibm-cloud-security/policy-enforcer-mixer-adapter

[img-coveralls-master]: https://coveralls.io/repos/github/ibm-cloud-security/appid-serversdk-nodejs/badge.svg
[url-coveralls-master]: https://coveralls.io/github/ibm-cloud-security/appid-serversdk-nodejs

[img-codacy]: https://api.codacy.com/project/badge/Grade/3156f40a37cb4026a443082fc1afcaa4?branch=master
[url-codacy]: https://www.codacy.com/app/ibm-cloud-security/appid-serversdk-nodejs