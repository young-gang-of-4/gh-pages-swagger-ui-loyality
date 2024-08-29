# gh-pages-swagger-ui-experiment

This is an experiment of hosting the Swagger-UI as GH pages, so it can be used to display Swagger documentation for APIs for a repository containing the OpenAPI/Swagger definition.

The repository is structured as follows:

- `api-docs` - directory containing the Swagger-UI
- `swagger.json` - the OpenAPI/Swagger definition
- `README.md` - this file (documentation describing the experiment)

## Recipe

When the repository was set up the following steps were taken:

First a directory for the Swagger-UI was created:

```bash
mkdir api-docs
```

The Swagger-UI was downloaded and the relevant files where extracted into the `api-docs` directory:

1. Downloaded the swagger-ui, do note the version number was the one available at the time of the experiment, do fetch the newest version available:

```bash
curl -X GET https://github.com/swagger-api/swagger-ui/releases/tag/v5.17.14
```

The files are unpacked:

```bash
tar xvzf swagger-ui-5.17.14.tar.gz
```

The files are copied to the `api-docs/` directory created above:

```bash
cd swagger-ui-5.17.14
cd dist # navigate to the dist directory
cp -r . ../../api-docs # copy the files to the api-docs directory recursively
cd ../../ # skip back to the root of the repository
```

You can all the directory what you want. The name `api-docs` is just a suggestion.

The `dist/` directory contains the Swagger-UI files, which can be used to serve the Swagger documentation as a static site.

From the [documentation][SWAGGERUI] (see: "Plain old HTML/CSS/JS (Standalone)" section):

> Open swagger-initializer.js in your text editor and replace "https://petstore.swagger.io/v2/swagger.json" with the URL for your OpenAPI 3.0 spec.

Since I do not have anything sharable at the moment, I will use the Swagger Petstore example:

But to demonstrate that it is possible to use a local file, I will use the `swagger.json` file in the repository.

First we dowmload the referenced file:

```bash
curl -X GET -o swagger.json https://petstore.swagger.io/v2/swagger.json
```

We edit the `swagger-initializer.js` file and add the path to the `swagger.json` file:

```javascript
url: "../swagger.json",
```

Since we can [serve multiple API definitions][MULTIPLE], we can add multiple URLs to the `urls` array in the `swagger-ui-bundle.js` file:

```javascript
    urls: [
      {
        url: "../swagger.json",
        name: "The local file from the repository"
      },
      {
        url: "https://jonasbn.github.io/gh-pages-swagger-ui-experiment/swagger.json",
        name: "The local Swagger Petstore"
      },
      {
        url: "https://petstore.swagger.io/v2/swagger.json",
        name: "The original Swagger Petstore"
      },
    ],
```

When the changes have been committed and pushed and the GitHub pages have been enabled for the repository, the Swagger-UI can be accessed using the following URL:

```html
https://jonasbn.github.io/gh-pages-swagger-ui-experiment/api-docs/
```

So now we serve the Swagger-UI as a static site using GH pages.

It works as expected and is fetching the `swagger.json` file from the repository in addition to the remote file and the file we service our selves, just as a proof of concept.

## Resources and References

- [SwaggerUI installation][SWAGGERUI]
- [StackOverflow: Swagger UI with Multiple URLs][MULTIPLE]

[SWAGGERUI]: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation
[MULTIPLE]: https://stackoverflow.com/questions/44816594/swagger-ui-with-multiple-urls
