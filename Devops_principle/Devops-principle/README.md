# Devops

Before devops 
    software developement was mess:
        - Developers wrote code and threw it over the wall to Ops.
        - Ops had no idea how the code worked.
        - Deployments broke.
        - Releases were once every few months.
        - Zero automation, all manual steps
        - Dev blamed Ops. Ops blamed Dev.

Evaluations Of Devops
    A guy named Patrick Debois organized the first DevOpsDays in Belgium.
    That event connected developers + operations and created the word DevOps.


2009 – DevOps term introduced
2010–2012 – CI/CD tools grow (Jenkins, Git)
2013–2014 – Infra-as-code (Chef, Puppet, Ansible, Terraform)
2015–2018 – Containers & Docker make deployments easier
2019+ – Kubernetes becomes the standard for DevOps delivery
Now – GitOps, automation everywhere, cloud-native everything


CORE PRINCIPLES:

1.Collaboration (the Culture Part Everyone Messes Up):
    Most teams say they collaborate, but in reality:
    Dev and Ops sit in different silos
    Dev says “it works on my machine”
    Ops says “your code broke the server”
    QA finds bugs late
    Security gets involved at the last minute   
That is anti-DevOps.
 
What Collaboration actually means:
👉 Developers, Ops, QA, and Security work as one unit, share responsibility, and communicate continuously.

Pratical examples:
    Development understand deployment + infra basics
    Operations understand the application flow
    joint stand-ups,shared dashboards
    Everyone owns uptime,reliability,releases.

2.Automation:
    If your process rely on humans pressing buttons,copying files,editing configs manually

Automation removes:
    human errors,bottlenecks,repetitive tasks,manual deployment and the slow releases

Automation means :
    CI/CD runs automatically 
    tests run automatically
    Builds and deployments 
    Infrastructure is created with Iac (Terraform,cloud formation,etc)
    Monitoring ,scaling and rollbacks ->automated
    Zero manual server setups

A devops pipeline with manual approvals everywhere is just a slow pipeline pretending to be modern.

3.Continuous Feedback:
    If you deploy and find issues hours later -> your feedback loop is broken.
    Feedback must be:
        instant
        automated
        actionable
    
    where feedback comes from:
        build failtures(CI)
        automated tests
        linting/code quality checks
        observability dashboards
        logs,metrics,traces
        monitoring and alerting
        user analytics

************************************************


DEVOPS LIFECYCLE STAGES

1.Plan: (Identity what to build)
    This is the thinking and planning stage

    mainly in this stage what will happen means :
        - Requirements gathering (bussiness + tech)
        - Creating user stories / tasks
        - Prioritizing features
        - Architecture planning
        - Sprint planning (if Agile)

    In this stage main goal is to be "Have a clear, small, well-defined piece of work that can move to development."

    Tools:
        Jira,Trello,Azure Boards,Github Projects,Confluence

2.CODE : (write the application)    FREQUENT COMMITS -> smooth CI
    Developer actually write the code here

    What happens :
       - Implement features
       - Fix bugs
       - Write unit tests
       - Peer code review
       - Version control commits

    Produce clean, reviewed code ready for the pipeline.

    Tools:
        Git,Github,Gitlab,Bitbucket
        IDE

3.BUILD : (Convert code into executable artifacts)

    In this stage,CI pipeline starts build the code 

    What happens:
        - Compile the code,
        - Install dependencies
        - Package into artifacts (JAR, WAR, ZIP, container image)
        - Create Docker images (if containerized)

    Finally this stage produce a build that can be tested and deployed

    Tools:
        Maven,Gradle,npm
        Jenkins,Github Actions,
        Docker

    Common issue: If build fails → the developer must fix immediately. CI enforces discipline.

4.TEST :   (Verify the build)
    Automation hits hard here

    In this stage ,what will happened means,
        Unit tests
        Integration tests
        API tests
        Security scans
        Code quality checks
        Linting
        Static analysis (SAST)

    Catch bugs early so bad code never reaches users.

    Tools:
        JUnit, Selenium, pytest
        SonarQube
        OWASP tools
        Jenkins/GitHub Actions test jobs

    Issues:If tests fails,pipeline stops ,no deployment

5.DEPLOY : (Push to staging or Production)
    Deployment becomes automatic in Devops
    
    In this stage,what happened here means
        Deploy to staging
        Deploy to production
        Canary Deployment
        Blue -Green deployment
        Automated rollbacks
        Configuration updates

    Deliver the release to real users with zero manual steps.

Tools:
    Tools:
        Kubernetes, Helm, ArgoCD
        Jenkins, 
        Docker, ECS, 

6.OPERATE: (Run application in production )

    once deployed,the app must be stable and fast
    
    In this stage,
        Manage servers/clusters
        Handle scaling
        Track resource usage
        Optimize performance
        Apply patches
        Handle incidents

    Keep the app healthy and reliable

    Tools:
            Kubernetes
            AWS/GCP/Azure services
            Ansible/Terraform
            Service meshes (Istio)

7.MONITOR : (Observe everything)
    
    Monitoring is the backbone of “continuous feedback.”

    what happened:
        Collect logs
        Collect metrics
        Track application performance
        Trigger alerts
        Detect failures early
        Monitor user experience

    Find issues before users complain

Tools:
    Prometheus,Grafana
    ELK,Loki
    New Relic
    Cloud watch

Feedback from this stage goes back to the plan.that's why it is called continuous lifecycle

*****************************************************************

CI/CD AUTOMATION OVERVIEW:

CI : (Automation for Developers)
    Automatically build, test, and validate code every time a developer pushes changes.

    Purpose:
        Catch problems early and keep the main branch stable.

    What CI automates:
        Pull latest code
        Build the application
        Run unit tests
        Run integration tests
        Run linting and code quality checks
        Run security scans
        Generate reports
        Block bad code from moving forward (stop pipeline if anything fails)

    CI removes the Merge conflicts,Broken builds,Last-minute surprises,Manual testing chaos

Continuous Delivery: (Automation for Release)

    Purpose:    
        Ensure the application is always in a “ready-to-deploy” state.

    What CD automates:

        Artifact packaging
        Versioning
        Publishing to artifact repositories
        Deploying to staging environments
        Preparing approvals for production
        CD stops at “ready to deploy” — human approval is optional for prod.

CD removes:
    Manual packaging
    Manual deployment mistakes
    Slow release cycles

CI/CD is the automation engine that removes human errors, speeds up delivery, and keeps deployments reliable.

CD — Continuous Deployment (Automation to Production)
        Automatically prepare, release, and deploy applications to staging or production with minimal or zero manual steps.
        This is the fully automated version of CD.

    What it automates:
        Deployment to staging
        Deployment to production
        Rollbacks
        Health checks
        Blue-green, canary, or rolling deployments
    No human approval needed.
    Every passing build → automatically deployed to production.

**********************************************************************************************

INFRASTRUCTURE AS CODE

    IaC means managing and provisioning your infrastructure (servers, networks, databases, load balancers, etc.) using code instead of manual clicks.

    example :
        Instead of creating servers, networks, VMs, databases manually in a cloud portal, you describe them as code.then the tool automatically creates exactly what you defined
        Best way to use the iac is terraform ,in there we declare the declarative Iac


******************************************************************************

IMMUTABLE INFRASTRUCTURE CONCEPT:

    Immutable means Something that cannot be changed or modified once after created
    Immutable Infrastructure means servers/VMs/containers are NEVER modified after deployment.
        If you need a change → you replace the entire server with a new one.
    
    Before Immutable ,there is tradditional ways that 
        that is the mutable way ,
            A VM is running in production
            You SSH into it
            You install software updates
            You edit config files
            You restart services
        After 6 months:
        Every VM is different.
        You can't reproduce the same server again.
        Debugging becomes a nightmare.

    Immutable (DevOps Modern Way)
        Build a new image (with Packer, Docker, etc.)
        Deploy this new image
        Route traffic to it
        Terminate the old server

    No manual changes.
    No SSH.
    No configuration drift.

****************************************************************************

CONFIGURATION MANAGEMENT :
    It is keeps the Keeping servers, systems, and environments consistent, predictable, and correctly configured — automatically.

    (we don’t log in manually to fix or configure anything ,we can automate it.)


    What Configuration management actually do means
        It can :
            Install packages
            Start/stop services
            Manage users
            Configure files
            Apply patches
            Enforce system state
            Fix drift automatically

    Example : It I want to install the java on 20 servers ,It takes more time and I ssh into 20 servers,install manually,config manually.
              That's where Cm comes into picture
                    You write one playbook
                    Ansible applies it to all 20 servers automatically
                    Every server ends up identical
                    No errors, no excuses



CONTAINERIZATION:
    Packaging your application with everything it needs (dependencies, libraries, runtime) into a single lightweight, isolated unit called a container.

    Example:
        without container:
            Developer uses python 3.10
            Server has python 3.7
            App crashes

        With help of container:
            Dockerfile define the python 3.10
            Container uses same environment everywhere
            zero surprises

********************************************************************************

MONITORING AND FEEDBACK LOOP

Monitoring = constantly watching your system, applications, and infrastructure to detect issues early.

Feedback loop = using the monitoring information to FIX the problem quickly and IMPROVE the system continuously.

What Feedback Loop means (real explanation)
    we take monitoring data → understand what broke → fix it → improve the next release.

Continuous cycle:
    Monitor → Detect → Notify → Fix → Learn → Improve


Monitoring detects issues early; feedback loops ensure teams fix the root cause and keep improving the system. Together they prevent repeated failures and keep the application reliable.


**************************************************************************************


COMMUNICATION AND COLLABORATION

    Agile + Scrum — How They Fit into DevOps

    Agile gives the mindset.
    Scrum gives the process.
    DevOps gives the automation + culture.

They work together like this:

Agile → Small, iterative development
Scrum → How teams organize that work 
DevOps → Automate releasing that work continuously

SCRUM:

1.Daily Standup:
    Purpose:
        Quickly update
        Identify blockers
        Sync on what's happening
    NOT a storytelling session.


Just 3 answers:

    What you did yesterday
    What you will do today
    What’s blocking you

It improves short-term communication.


2.Sprint Planning: (Agree on What to Build)

Purpose:
    Decide what features/tasks to build this sprint
    Break work into clear tasks

This keeps everyone aligned on “what exactly are we building?”

3.Sprint Review:
    Purpose:

        Demo what was built
        Get feedback
        Show progress to stakeholders

    This improves transparency.

4.Sprint Retrospective: (Improve Communication)

    Purpose:

        Discuss what went wrong
        Improve teamwork
        Avoid repeating mistakes next sprint

    This improves team collaboration & culture.

***************************************
DevOps Toolchain Overview (Simple Explanation)

A DevOps toolchain is a set of tools that work together to help developers and operations teams build, test, deliver, and monitor software faster and more reliably.

The toolchain is usually divided into 6 major stages:
    1.Plan
    2.Code
    3.Build
    4.Test
    5.Release/Deploy
    6.Monitor & Operate


DIAGRAM:

    Plan → Code → Build → Test → Release → Deploy → Monitor
            ↑                                            ↓
            └─────────────────Feedback Loop──────────────┘
