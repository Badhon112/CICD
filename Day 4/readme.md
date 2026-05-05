## Jenkins

```
docker run -d \
 -p 8080:8080 -p 50000:50000 \
 -v jenkins_home:/var/jenkins_home \
 --name jenkins \
 jenkins/jenkins:lts

```

- echo $JENKINS_HOME
- It will give the path where the data will stored
- When we create a job the content of that job folder is created in the workspace

- Control Plane (Controller)
  - Stores state : jobs, build, credentials, plugins.
  - Orchestrates queue, scheduling, labels, security, UI/API
  - Executors = 0 in production: no build here.
  - Backup $JENKINS_HOME: upgrades and config live here
  - Dispatches work to agent : receives results and logs

- Data Plane (execution, Agents)
  - Run build steps ; use remote root workspaces
  - Provide capacity via executors advertise capabilities with labels.
  - Ephemeral or static ; scale horizontally
  - Keep clean : cleanWs(), monitor disk, ship artifacts back

---

## Demo 1: Add Parameters (Boolean, Choice)

- Parameter code build with parameter
- boolean RUN_TESTS
- Choice Parameter
  - env
    - dev
    - stage
    - prod

```
echo "RUN_TESTS=$RUN_TESTS ENV=$ENV"
echo "Report for #$BUILD_NUMBER (env=$ENV)" > report-$ENV.txt
if ["$RUN_TESTS" = "true" ]; then
	echo "Running tests ..."; sleep 1; echo "OK"
else
	echo "Skipping tests."
fi
```

---

## Demo 2: Git SCM + Branch as a Parameter

- In the Parameter Section select String Parameterized
  - NAME=BRANCH
  - Default value = BADHON112
- In Source Code Management select GIT add the url and Branches to build $BRANCH

- Build Steps run this shell script

```
echo "Built from BRANCH = $BRANCH"
git --version
echo "Latest commit:"
git log --oneline -n 1 || tre
echo "Jenkins vars : GIT_BRANCH = $GIT_BRANCH GIT_COMMIT = $GIT_COMMIT"
```

https://prnt.sc/UqYtWxn08cMZ
https://prnt.sc/lAqYMEdL5aga

---

## Pool SCM Trigger (no webhooks)

## Webhook Trigger (GitHub/GitLab)

https://prnt.sc/RF3HQKfFrOg-

## Demo 5: Scheduled Nightly (Cron) + Workspace Cleanup
