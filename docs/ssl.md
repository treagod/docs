Grip has built-in and easy to use SSL support, it can be configured easily and deployed instantly.

To start your Grip application with SSL support, use:

```bash
crystal build --release src/your_app.cr
./your_app --ssl --ssl-key-file your_key_file --ssl-cert-file your_cert_file
```
