# GoCD Summary
## What we achieved:
- git clone
- compile codebase
- package
- upload to Artifactory

## Pipeline as code
```yaml
environments:
  example:
    environment_variables:
      EXAMPLE_DEPLOYMENT: testing
    pipelines:
      - silberfishle
pipelines:
  silberfishle:
    group: simple
    materials:
      mygit:  # this is the name of material
        # says about type of material and url at once
        git: https://github.com/cicd-hackathon-stgt/gs-spring-boot.git
    stages:
      - build: # name of stage
          jobs:
            chmod: # name of the job
              tasks:
                - exec: # indicates type of task
                   command: /bin/sh
                   arguments:
                    - "-c"
                    - "chmod +x mvnw"
            install: # name of the job
              tasks:
                - exec: # indicates type of task
                   command: /bin/sh
                   arguments:
                    - "-c"
                    - "./mvnw clean install"
            archive: # name of the job
              tasks:
                - exec: # indicates type of task
                   command: /bin/sh
                   arguments:
                    - "-c"
                    - "./mvnw -s settings.xml deploy"
```

## What we struggled with:
- no self descriptive ui
- too many clicks to get the console log
- documentation of yml config for pipelines
- agent configuration
- multiple exec commands in one task
- semantics for pipelines is quiet difficult

## Positive
- rudimental pipeline could be done in 1 afternoon
- AMI to get youself ready in an instant