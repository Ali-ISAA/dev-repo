# Development Repository (dev-repo)

## Overview
Primary repository for active development. Developers create feature branches, open pull requests, and merge code to the `main` branch.

## Purpose
- Active code development
- Feature branch workflow
- Pull request reviews
- Unit testing and local validation
- CI/CD trigger point for test environment

## Workflow

### Development Process
1. Clone the repository
2. Create a feature branch from `main`
3. Develop and commit changes
4. Open a pull request for review
5. Merge to `main` after approval

### Automatic Deployment
When code is merged to `main`:
- GitHub Actions workflow triggers automatically
- Runs tests and builds
- Deploys code to **test-repo** for QA validation
- Excludes `.github/workflows/` and `README.md` from deployment

## Repository Structure
```
dev-repo/
├── .github/
│   └── workflows/
│       └── deploy-to-test.yml    # Auto-deploys to test-repo
├── app.js                         # Main Express application
├── public/                        # Static files (HTML, CSS)
├── tests/                         # Jest test suite
├── Dockerfile                     # Multi-stage build with tests
├── package.json
└── README.md                      # This file (not synced)
```

## Local Development

### Prerequisites
- Node.js (v14 or higher)
- npm

### Setup
```bash
npm install
```

### Run Tests
```bash
npm test
```

### Start Application
```bash
node app.js
```

The application runs on `http://localhost:3000`

### Key Endpoints
- `GET /` - Landing page
- `GET /health` - Health check
- `GET /api/status` - Operational status
- `POST /api/data` - Data processing

## Docker Build
```bash
docker build -t dev-app .
docker run -p 3000:3000 dev-app
```

## CI/CD Pipeline
**Current Position**: START of pipeline

```
[dev-repo] --automatic--> [test-repo] --manual--> [prod-repo]
    YOU ARE HERE
```

### Next Stage
After merge to `main`, code automatically deploys to:
- Repository: `test-repo`
- Purpose: QA testing and validation
- Trigger: Automatic via GitHub Actions

## Environment-Specific Files
The following files are **NOT** deployed to downstream environments:
- `.github/workflows/*` - Workflow configurations
- `README.md` - Repository-specific documentation

## Contributing
1. Follow feature branch naming: `feature/description` or `fix/description`
2. Write meaningful commit messages
3. Ensure all tests pass before opening PR
4. Request code review from team members
5. Address review comments before merging

## Secrets Required
- `TEST_REPO_PAT` - Personal Access Token for deploying to test-repo

## Support
For issues or questions, please open an issue in this repository.
