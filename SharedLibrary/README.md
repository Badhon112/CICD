## Jenkins shared Library Explained

- Too many pipelines repeat identical CI/CD steps everywhere
- Changing a standard step requires editing every project (JenkinsFile)
- Inconsistencies appear when teams copy/paste pipeline code
- Updating tool URLs or credentials becomes slow and risky
- Scaling pipelines across many microservices becomes unmanageable
- Central teams struggle to enforce organization wide pipeline standers.

## A jenkins shared Library is a central, version-controlled repository for reusable and standardized pipeline logic
- A central repo to store reusable pipeline logic
- Standardizes CI/CD steps across many projects.
- Version-controlled library pipelines can be imported by Jenkinsfile
- Single source of truth for build, test, deploy, scans(SAST/DAST), and image ops.

