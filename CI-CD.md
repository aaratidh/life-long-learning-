## What is CI/CD ?
- Continious Integration and Continious Development
- Where code is push in common repository and code is build by automated build the relased in market through deployment.
- Tools used are Jenkins, github, gitlab, gitActions
- Work looks like:
    - Source code management: Github, git actions
    - Build applications : Code gets complied, runs packages installation, build includes Unit Test
    - Deployed application : Build application into web , this includes integration testing, UI testig
- CI/CD Category Looks like:

  
| Category                      | Tools                                | Use                                                                       |
| ----------------------------- | ------------------------------------ | ------------------------------------------------------------------------- |
| **Version Control**           | GitHub / GitLab / Bitbucket          | Instead of (or in addition to) CodeCommit                                 |
| **CI/CD Engine**              | Jenkins / GitLab CI / GitHub Actions | Alternative to CodePipeline; supports custom runners, complex build logic |
| **Data Quality / Validation** | Great Expectations, dbt tests,dquee  | Validate data correctness as part of CI/CD                                |
| **Infrastructure as Code**    | Terraform                            | Multi-cloud IaC alternative to CloudFormation                             |
| **Artifact Repository**       | Nexus / Artifactory                  | Store Python packages or ETL wheel files                                  |
| **Monitoring / Alerting**     | Datadog / Prometheus / Grafana       | Enhanced observability beyond CloudWatch                                  |

  
