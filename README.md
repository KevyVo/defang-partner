# ekai - Cloud Setup Portal

A static web application that guides users through connecting their AWS account to [ekai](https://yourekai.com) via a step-by-step wizard. It creates the necessary CloudFormation stack with IAM roles for CI/CD integration using GitHub Actions OIDC.

## How It Works

1. User receives an invite link and enters their invite ID on the landing page
2. The wizard validates the invite against the Defang API
3. User provides their AWS Account ID and preferred region
4. The app generates a CloudFormation Quick Create URL and opens the AWS console
5. After the stack is created, the user confirms to complete the setup

## Project Structure

```
├── index.html          # Landing page with invite ID form
├── cloud-setup.html    # Multi-step AWS setup wizard
├── main.js             # Wizard logic and Defang API integration
├── main.css            # Styles (ekai brand tokens)
├── assets/             # Logos and favicon
├── nginx.conf          # Nginx config with routing rules
├── Dockerfile          # Nginx-based container image
├── compose.yaml        # Docker Compose service definition
└── .github/workflows/
    └── defang.yaml     # CI/CD pipeline using Defang GitHub Action
```

## Running Locally

Build and run with Docker:

```sh
docker build -t ekai-cloud-setup .
docker run -p 8080:8080 ekai-cloud-setup
```

Or with Docker Compose:

```sh
docker compose up
```

Then visit `http://localhost:8080`.

## Deployment

This project deploys via [Defang](https://defang.io) using the GitHub Actions workflow in `.github/workflows/defang.yaml`. Pushing to `main` triggers a deployment to your created stack with the portal workflow. You can also manually trigger deployments (up/down) for any stack via the workflow dispatch.