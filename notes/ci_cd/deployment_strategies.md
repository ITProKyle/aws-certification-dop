# Deployment Strategies

## Single Target Deployment

- build and deploy to single target
- used for small deployment projects
  - legacy
  - non-high-availability
- new versions are installed directly to the target server
- brief outage occurs during install
  - caused by lack of secondary servers
- testing is limited
- rollback involves removing the new version and installing the previous

## All-at-Once Deployment

- similar to [Single Target Deployment](#single-target-deployment) but with multiple targets
- more complex than [Single Target Deployment](#single-target-deployment), often requiring orchestration tooling
- same negatives as [Single Target Deployment](#single-target-deployment)

## Minimum in-service Deployment

- build and deploy to targets ensuring that _x_ number of targets remain in-service (active/usable) throughout deployment
  - uses health checks to verify when servers are in-service
  - deployments happen to as many targets as possible
- happens in multiple _stages_
- orchestration is required
- allows for automated testing
  - targets are tested prior to continuing
- generally no downtime

## Rolling Deployment

- deploys to _x_ number of targets per _stage_
  - uses health checks
- requires significant automation and orchestration
- orchestration is required
- allows for automated testing
  - targets are tested prior to continuing
- least time efficient
- does not factor in overall health of the application across all targets
- generally no downtime assuming the number of targets per run isn't large enough to impact the application
- can be paused
  - allows for multi-version testing

## Blue Green Deployment

AKA A/B deployment

- deploys to an entirely new environment (infrastructure, etc) each run
  - uses health checks
  - redirects traffic to the new environment when it is ready to go live
  - destroys the old environment after the new environment is live (can be delayed)
- requires advanced orchestration tooling (infrastructure as code, etc)
  - fully automated
- carries significant cost to maintain two environments
- deployment process is quick, happens all at once
- cutover and migration is clean and controlled (DNS change)
- rollback is equally clean, DNS regression
- health and performance of entire environment can be tested prior to cutover
- does **NOT** support A/B testing

## Canary Deployment

- similar to [Blue Green Deployment](#blue-green-deployment)
  - both environments are live at the same time
  - traffic is gradually shifted to the new environment over time
    - weighted round robin (Route 53)
    - users become QA/load testers
- supports A/B testing
