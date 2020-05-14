# S3 Cache Buildkite Plugin

Save and restore cache to and from AWS S3.

## Example

Add the following to your `pipeline.yml`:

```yml
steps:
  - command: npm install && npm test
    plugins:
      - peakon/s3-cache#v1.0.0:
          save:
            - key: 'v1-node-modules-{{ checksum("package-lock.json") }}'
              paths: [ "node_modules" ] # required, array of strings
              when: always # optional, one of {always, on_success, on_failure}, default: on_success
          restore:
            - keys:
                - 'v1-node-modules-{{ checksum "package-lock.json" }}'
                - 'v1-node-modules-' # will load latest cache starting with v1-node-modules-
```

## Configuration


### Prerequisites

Make sure to set `BUILDKITE_PLUGIN_S3_CACHE_BUCKET_NAME=your-cache-bucket-name` before using this plugin.

### Plugin

You can specify either `save` or `restore` or both of them for a single pipeline step.

#### `save` properties


#### `restore` properties


#### Supported functions

- `checksum 'filename'` - sha256 hash of a `filename`

- `epoch` - time in seconds since Unix epoch (in UTC)

- `.Environment.SOME_VAR` - a value of environment variable `SOME_VAR`


## Developing

To run the tests:

```shell
docker-compose run --rm tests
```

## Contributing

1. Fork the repo
2. Make the changes
3. Run the tests
4. Commit and push your changes
5. Send a pull request
