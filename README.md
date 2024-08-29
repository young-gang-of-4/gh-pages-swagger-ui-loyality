# gh-pages-swagger-ui-experiment

This is an experiment on embedding the swagger-ui as GH pages

## Recipe

1. Downloaded the swagger-ui: https://github.com/swagger-api/swagger-ui/releases/tag/v5.17.14

2. `tar xvzf swagger-ui-5.17.14.tar.gz`

3. cd swagger-ui-5.17.14
4. cd dist
5. cp -r . /Users/jonasbn/develop/github-jonasbn/gh-pages-swagger-ui-experiment/gh-pages

These are the docs for the swagger-ui: https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation/

6. Open swagger-initializer.js in your text editor and replace "https://petstore.swagger.io/v2/swagger.json" with the URL for your OpenAPI 3.0 spec.

## Resources and References

- [SwaggerUI installation](https://swagger.io/docs/open-source-tools/swagger-ui/usage/installation/)
