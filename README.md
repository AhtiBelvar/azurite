# Azurite Fork
This repository has been forked from [arafato/azurite](https://github.com/arafato/azurite) to workaround a particular issue with Table Storage.

:warning: **Warning: This is not an actively maintained repository. Where possible please use the new azurite project located at [https://github.com/azure/azurite](https://github.com/azure/azurite)**

## Docker image

### Pulling from Docker Hub
Every release of Azurite starting with version 0.9.7 is available at [Docker Hub](https://hub.docker.com/r/ahtibelvar/azurite/) and ready to be pulled with:
```bash
$ docker pull ahtibelvar/azurite
```
Please note that the `latest` tag will always refer to the latest release.

### Build the Docker image 
To build the Docker image yourself, execute the following:
```bash
$ docker build -t ahtibelvar/azurite .
```

### Run the Docker image
To run the Docker image, execute the following command:
```bash
$ docker run -d -t -p 10000:10000 -p 10001:10001 -v /path/to/folder:/opt/azurite/folder ahtibelvar/azurite
```

#### Configure the executable when running the container
By default, the container starts all services available (currently blob, queue, and table).
Using the environment variable `executable`, specific executables can be specifed:

 * `blob` Start the Blob Storage Emulator only
 * `queue` Start the Azure Queue Storage Emulator only
 * `table` Start the Azure Table Storage Emulator only

##### Usage example:
```bash
$ docker run -e executable=blob -d -t -p 10000:10000 -v /path/to/folder:/opt/azurite/folder ahtibelvar/azurite
```

## Usage with Azure Cross-Platform CLI 2.0

To perform blob storage operations using the 2.0 Azure cross-platform CLI, you need to operate with the
appropriate connection string. The values within are based on the hardcoded Azure Storage Emulator values.

Example command to create a container:

```shell
$ az storage container create --name 'test' --connection-string 'DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;'

{
  "created": true
}
``
