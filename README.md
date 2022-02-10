# DTSflat-server

Minimal computing server for a [DTS API](https://distributed-text-services.github.io/specifications/) from a DTSflat file structure.

The server supports the DTS Navigation Endpoint and Documents Endpoint.

The DTSflat files can be generated from a TEI XML file using https://github.com/robcast/simple-tei2dtsflat

The server uses a simple [Nginx](http://nginx.org/) configuration to serve pre-generated files without additional active components.

## Required

- [Docker](https://www.docker.com/)
- [docker-compose](https://docs.docker.com/compose/)

Alternatively you can use the Nginx config with an existing Nginx server without Docker.

## Configuration

```
cp .env.template .env
```

Edit the `.env` file to add your server hostname in `VIRTUAL_HOST` and the path to the directory with the DTSflat files in `DTS_DATA_DIR`.

## Run

```
docker-compose up -d
```

The DTS API will be accessible through your hostname: 

- http://your.host.name/dts/navigation/?id=your-document-id
- http://your.host.name/dts/documents/?id=your-document-id

## Optional configuration

Optional configuration variables that can be added to the `.env` file:

- `API_BASE_PATH` first part of all endpoint URIs. Default: "/dts". Must match the URIs in the generated DTSflat files!
- `DOCUMENT_API_PATH` second part of the Document Endpoint URI. Default: "/documents". Must match the URIs in the generated DTSflat files!
- `NAVIGATION_API_PATH` second part of the Navigation Endpoint URI. Default: "/navigation". Must match the URIs in the generated DTSflat files!

## DTS API limitations

- Currently no support for HTTP headers (could have limited support #1).
- No support for ranges like `start` and `end` in the Document Endpoint and the Navigation Endpoint.
- No support for result pagination with `max` in the Navigation Endpoint.
- No support for customization of the result with `groupBy` or `exclude` in the Navigation Endpoint.
- Currently no Collection Endpoint (could be supported).
