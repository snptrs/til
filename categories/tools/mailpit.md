# Mailpit

Mailpit provides a local SMTP server and webmail interface, making it simple to test mail functionality in development.

## Install and configure

- Install with Homebrew: `brew install mailpit`
  - To configure it to automatically run in the background: `brew services start mailpit` (and `brew services stop mailpit` to remove the launch agent).
- By default, the web ui will be on [http://0.0.0.0:8025](http://0.0.0.0:8025) and the SMTP server will be on `0.0.0.0:1025`.
  - Start on different ports: `mailpit --smtp [::]:8125` and `mailpit --listen [::]:8126`

## Configuring apps to use it

- If developing in a Docker container, use `host.docker.internal` as the server address so that it looks for it on the host rather than in the container.
