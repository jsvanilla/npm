# @semantic-release/npm

Set of [semantic-release](https://github.com/semantic-release/semantic-release) plugins for publishing to a [npm](https://www.npmjs.com/) registry.

[![Travis](https://img.shields.io/travis/semantic-release/npm.svg)](https://travis-ci.org/semantic-release/npm)
[![Codecov](https://img.shields.io/codecov/c/github/semantic-release/npm.svg)](https://codecov.io/gh/semantic-release/npm)
[![Greenkeeper badge](https://badges.greenkeeper.io/semantic-release/npm.svg)](https://greenkeeper.io/)

## verifyConditions

Verify the presence of the `NPM_TOKEN` environment variable, create or update the `.npmrc` file with the token and verify the token is valid.

## getLastRelease

Determine the last release of the package on the `npm` registry.

## publish

Publish the package on the `npm` registry.

## Configuration

### Environment variables

The `npm` authentication configuration is **required** and can be set via environment variables.

Both the [token](https://docs.npmjs.com/getting-started/working_with_tokens) and the legacy (`username`, `password` and `email`) authentication are supported. It is recommended to use the [token](https://docs.npmjs.com/getting-started/working_with_tokens) authentication. The legacy authentication is supported as the alternative npm registries [Artifactory](https://www.jfrog.com/open-source/#os-arti) and [npm-registry-couchapp](https://github.com/npm/npm-registry-couchapp) only supports that form of authentication at this point.

| Variable       | Description                                              
| -------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `NPM_TOKEN`    | Npm token created via [npm token create](https://docs.npmjs.com/getting-started/working_with_tokens#how-to-create-new-tokens) |
| `NPM_USERNAME` | Npm username created via [npm adduser](https://docs.npmjs.com/cli/adduser) or on [npmjs.com](https://www.npmjs.com)           |
| `NPM_PASSWORD` | Password of the npm user.                                                                                                     |
| `NPM_EMAIL`    | Email address associated with the npm user                                                                                    |

Use either `NPM_TOKEN` for token authentication or `NPM_USERNAME`, `NPM_PASSWORD` and `NPM_EMAIL` for legacy authentication

### Options

The plugins are based on `npm` and will use the configuration from [`.npmrc`](https://docs.npmjs.com/files/npmrc). See [npm config](https://docs.npmjs.com/misc/config) for the option list.

The [`registry`](https://docs.npmjs.com/misc/registry) and [`dist-tag`](https://docs.npmjs.com/cli/dist-tag) can be configured in the `package.json` and will take precedence over the configuration in `.npmrc`:
```json
{
  "publishConfig": {
    "registry": "https://registry.npmjs.org/",
    "tag": "latest"
  }
}
```

### Usage

The plugins are used by default by [semantic-release](https://github.com/semantic-release/semantic-release) so no specific configuration is requiered to use them.

Each individual plugin can be disabled, replaced or used with other plugins in the `package.json`:
```json
{
  "release": {
    "verifyConditions": ["@semantic-release/npm", "verify-other-condition"],
    "getLastRelease": "custom-get-last-release",
    "publish": ["@semantic-release/npm", "custom-publish"]
  }
}
```
