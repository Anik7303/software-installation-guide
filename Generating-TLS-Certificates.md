# Generate TLS Certificates (for local development only);

## Using `mkcert`:

- Install `mkcert` - [Instructions](/Software%20Installation%20Guide.md#mkcert)
- Add `mkcert` to your local root CAs.

```bash
# This generates a local certifictate authority (CA). This CA is only trusted locally in your device
mkcert -install
```

- Generate a certificate for your site, signed by mkcert

```bash
mkcert localhost

# if you're using a custom hostname eg. example.com
mkcert example.com
```

- Configure your server using the generated files.
