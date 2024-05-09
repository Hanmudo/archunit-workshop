# archunit-workshop
Home of the ArchUnit Workshop

Follow the link to the [presentation](https://hanmudo.github.io/archunit-workshop/).

Usage of the presentation locally see: https://github.com/webpro/reveal-md#docker .

## Docker

You can use Docker to run this tool without needing Node.js installed on your machine. Run the public Docker image,
providing your markdown slides as a volume. A few examples:

```bash
docker run --rm -p 1948:1948 -v $(pwd)/slides:/slides webpronl/reveal-md:latest
docker run --rm -p 1948:1948 -v $(pwd)/slides:/slides webpronl/reveal-md:latest --help
```

The service is now running at [http://localhost:1948][2].

To enable live reload in the container, port 35729 should be mapped as well:

```bash
docker run --rm -p 1948:1948 -p 35729:35729 -v $(pwd)/slides:/slides webpronl/reveal-md:latest /slides --watch
```

To run the reveal instance with the custom script and css:
```bash
docker run --rm -p 1948:1948 -p 35729:35729 -v $(pwd)/:/slides webpronl/reveal-md:latest /slides --watch
```
