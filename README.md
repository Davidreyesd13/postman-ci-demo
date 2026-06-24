# JSONPlaceholder API Testing — Postman + Newman + CI/CD

API testing project demonstrating automated test execution with Postman, Newman, and GitHub Actions.

## What This Project Does

This project tests the [JSONPlaceholder](https://jsonplaceholder.typicode.com/) public API using a Postman collection, then automates that testing through a CI/CD pipeline that runs on every push.

**Pipeline flow:**
```
Postman Collection → Newman (CLI execution) → GitHub Actions → HTML Report
```

## What's Tested

- **GET requests** — fetching single resources and full collections
- **POST requests** — creating resources and validating response data
- **Status code validation** — 200, 201, 404
- **Data type validation** — verifying fields return expected types (string, number, object)
- **Nested object validation** — accessing and validating deeply nested fields (e.g. `address.geo.lat`)
- **Array validation** — checking array length and validating every item in a collection meets a condition (`forEach`)
- **Dynamic variables** — capturing a value from one response (like a created resource's ID) and reusing it in a later request

## Tech Stack

- **Postman** — designing requests and writing test assertions (`pm.test`, `pm.expect`)
- **Newman** — running the Postman collection from the command line
- **newman-reporter-htmlextra** — generating visual HTML test reports
- **GitHub Actions** — running the test suite automatically on every push or pull request

## Running Locally

**Prerequisites:** Node.js and npm installed.

```bash
# Install Newman and the HTML reporter
npm install -g newman newman-reporter-htmlextra

# Run the collection
newman run "JSONPlaceholder API.postman_collection.json" \
  -e JSONPlaceholder.postman_environment.json \
  -r cli,htmlextra \
  --reporter-htmlextra-export newman/report.html
```

## CI/CD Pipeline

Every push to `main`/`master` (and every pull request) automatically triggers a GitHub Actions workflow that:

1. Spins up a fresh Ubuntu environment
2. Installs Node.js and Newman
3. Runs the full Postman collection
4. Generates an HTML report
5. Uploads that report as a downloadable artifact

See [`.github/workflows/api-tests.yml`](.github/workflows/api-tests.yml) for the full configuration.

## Why This Project

This was built as a hands-on learning project to go from manual Postman testing to a fully automated API testing pipeline — covering the core skills used in real QA Automation workflows: writing meaningful assertions, organizing test collections, and integrating tests into CI/CD so they run without manual intervention.

## Author

**David Reyes** — QA Engineer focused on manual testing and growing into automation (Postman, Selenium, CI/CD).
[GitHub](https://github.com/Davidreyesd13)
