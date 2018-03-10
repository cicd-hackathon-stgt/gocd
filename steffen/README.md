Links:
- [GoCD Documentation](https://docs.gocd.org/current)
- [GoCD Website](https://www.gocd.org)
- Slack Channel: #team-gocd

Breakdown:
- Concept of GoCD
- Common
- Setup (infrastructure)
- GUI pipeline
- Code pipeline

Concept of GoCD:
- everything is a pipeline
- requires source code(not possible to preconfigure pipelines without having configured a source before)
- pipelines can depend on each other and require them to be successful
- Stages can be run in parallel so you can't run stages who are depending on each other
- Stages are a collection of jobs similar to Jenkins

Common:
- Amount of agents is equal to stages (1 stage is running on 1 agent)
- Server - Agent communication is bidirectional
- Communication is running on port 8154
- all traffic is https encrypted (self signed certificate using the java keystore)

Setup:
- Possible to setup on
    - Windows
    - OSX
    - Debian/APT
    - RPM/YUM
    - Cloud Providers
    - AMIs
    - Docker
    - (basically any platform where Java Runtime Environment (JRE) version 8 is available)
- [Download site](https://www.gocd.org/download/)
- Example docker [docker-compose.yml](./docker-compose.yml)
- Agents have to be configured manually(Java JDK, Maven in our case in each docker container agent)

GUI Pipeline:
- Split up in 3 Steps: Basic settings, Materials and Stage/Job and are pretty self-explanatory
- Basic settings defines the pipeline group and pipeline name
- Materials defines the location of the source files
- Stage/Job requires you to name the stage and to add an initial job and task

Code Pipeline:
- Every pipeline you configure in the GUI gets stored as XML
- XML is structured in Pipelines->Stages->Jobs->Tasks
- Example XML is found [here](./godata/config/cruise-config.xml)


Code Pipeline (YAML/JSON):
- GoCD gives you the possibility to version your pipeline settings with YAML and JSON files
- [Documentation](https://docs.gocd.org/current/advanced_usage/pipelines_as_code.html)
- Advantages: you can version the pipeline
- Disadvantages: The plugins don't support different branches for the configuration while defined on the top-level and not per pipeline
