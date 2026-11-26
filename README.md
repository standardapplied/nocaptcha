# NoCAPTCHA

Replace CAPTCHA with single-use, disposable passkeys. Human-friendly bot prevention without the frustration.

To get a feel for the widget, checkout the [hosted demo](https://demo.singlr.ai/nocaptcha/)

![NoCaptcha](./nocaptcha.png)

## Programming languages and frameworks
The API is build in Java using Helidon 4.x. Powered by Java virtual threads. The UI is pure Javascript using Vite build tool.

## Build and run

### Prerequisites
- JDK 21 or newer (`java -version` should report 21+)
- Maven 3.8+

### Build
From the repository root:
```bash
mvn package          # compile, run the tests and build api/target/api.jar
mvn verify           # everything above plus checkstyle and SpotBugs, as CI does
```

### Run
The server reads `config.yaml` and `config-<profile>.yaml` from the current working
directory, so start it from the `api` directory:
```bash
cd api
java -jar target/api.jar
```

Once it logs `Singular nocaptcha is up at http://localhost:7080`:
- http://localhost:7080/ serves the demo page and the `nocaptcha.js` widget
- `POST /v1/nocaptcha/start` and `PUT /v1/nocaptcha/complete` on port 7080 are the API
- http://localhost:7085/health/ready and `/health/live` are the health checks

The default profile is `dev`. To pick another one (`dev`, `ci`, `staging`, `prod`), pass it as
the first argument (`java -jar target/api.jar prod`) or set `NOCAPTCHA_PROFILE`. The
`WAN_ID` and `WAN_ORIGINS` environment variables override the passkey relying party id and
allowed origins. The server logs a warning if they are unset, which is fine for local use.

### Debugging

For adding a debugger
```bash
java -agentlib:jdwp=transport=dt_socket,address=127.0.0.1:5005,suspend=n,server=y -jar target/api.jar
```

## Coding & naming conventions
We use the check style plugin and have adopted Google's check style [rules](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml)

Configure your IDE accordingly. To ensure that you have followed the conventions, run:
```bash
mvn validate
```

## Contributing

Contributions are welcome! Feel free to help enhance either the:
- Backend passkeys-based NoCaptcha implementation
- Frontend NoCaptcha widget
- Address the TODOs in the code

Just fork the repository and submit a pull request with your improvements.