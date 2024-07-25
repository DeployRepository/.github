# Welcome to DeployRepository

DeployRepository is dedicated to providing seamless and reliable deployment solutions for projects across multiple technologies, ensuring zero downtime and smooth operations.

## Our Mission

Our mission is to simplify the deployment process, making it accessible and efficient for developers at all levels. We strive to create tools that not only meet but exceed the needs of individual developers, small businesses, and large enterprises.

## Key Features

- **Zero Downtime Deployment**: Ensure uninterrupted service during deployments.
- **Multi-Technology Support**: Currently supporting Laravel, with more technologies being added.
- **Easy Integration**: Simple setup and integration into your existing workflow.
- **Flexible Deployment**: Suitable for projects of all sizes, from personal projects to enterprise applications.

## Getting Started

To get started with DeployRepository, check out our primary GitHub Action:

### DeployRepository/zero-downtime-deployment

A versatile action designed for zero downtime deployment of Laravel projects using SSH. 

```yaml
name: deploy to server

concurrency:
  group: production
  cancel-in-progress: true

on:
  release:
    types: [released]

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production

    steps:
      - name: Deploy Laravel project
        uses: DeployRepository/zero-downtime-deployment@v1.0.0
        with:
          host: ${{ secrets.REMOTE_HOST }}
          username: ${{ secrets.REMOTE_USER }}
          password: ${{ secrets.REMOTE_PASSWORD }}
          port: ${{ secrets.REMOTE_PORT }}
          target: '/home/www/test.com'
          sha: ${{ github.sha }}
          github_token: ${{ secrets.GH_TOKEN }}
          env_file: ${{ secrets.ENV_FILE }}
          run_script_after_download: |
              cd $THIS_RELEASE_PATH
              composer install --prefer-dist
              php artisan migrate --force
              php artisan storage:link
          run_script_before_activate: |
              cd $THIS_RELEASE_PATH
              php artisan optimize:clear
          run_script_after_activate: |
              cd $THIS_RELEASE_PATH
              php artisan optimize
```
Check more details [hire](https://github.com/DeployRepository/zero-downtime-deployment)

## This GitHub Action Is Sponsorware 💰💰💰
Originally, this github action was only available to my sponsors on GitHub Sponsors until I reached 100 sponsors.

<!-- Now that we've reached the goal, the github action is fully open source. -->

Enjoy, and thanks for the support! ❤️ [Become a sponsor](https://github.com/sponsors/DeployRepository) 

Learn more about Sponsorware at [github.com/sponsorware/docs](https://github.com/sponsorware/docs) 💰.

Your support helps us continue to develop and maintain high-quality deployment tools. Consider sponsoring us on [GitHub Sponsors](https://github.com/sponsors/DeployRepository):

- **$1 a month: Student** - Access to DeployRepository/zero-downtime-deployment with unlimited projects, deployments, and team members.
- **$5 a month: The Individual** - Access to DeployRepository/zero-downtime-deployment with unlimited projects, deployments, and team members.
- **$10 a month: The Generous Individual** - A higher contribution with the same access.
- **$25 a month: Small Business** - Ideal for small businesses.
- **$50 a month: Medium Business** - For medium-sized businesses.
- **$100 a month: Big Business** - For large enterprises.

## Join the Community

Stay updated and join the conversation:

- [Twitter](https://x.com/DeployRepo)

---

Thank you for visiting DeployRepository. We look forward to helping you achieve seamless and reliable deployments!
