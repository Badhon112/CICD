## What is Jenkins, and what is its primary use?

Jenkins is an open-source (CI\CD) automation server that simplifies the software development lifecycle by automating tasks like building, testing and deploying code.

- CI = Continuous Integration
  - Build & Test every push/PR automatically
  - Fast checks enforce merge protection on the branch
  - Compile, uit test, quick, Security/dependency scans.

- CD = Continuous Delivery
  - Keep main always deployable with versioned artifact.
  - Promote the same artifact across environment
  - Human approvals/gates before production.

- CDP = Continuous Deployment
  - Auto-deploy to prod when all checks pass

## What is a Jenkins Pipeline?

- A Jenkins Pipeline is an automated sequence of steps tat defines how code is build, tested, and deployed. Pipelines are written as code, typically inside a jenkins making them version-controlled and easy to share
