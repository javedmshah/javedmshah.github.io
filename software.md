---
layout: page
title: open-source projects
description: prototype code for enabling identity use cases. NOT for use in production!
---

<div class="navbar">
    <div class="navbar-inner">
        <ul class="nav">
            <li><a href="https://github.com/javedmshah">github</a></li>            
        </ul>
    </div>
</div>

---

#### <a name="https://github.com/javedmshah/impersonation-policy">impersonation</a>
**java** code to implement impersonation via helpdesk in openam. This is old code but demonstrative of how to implement "insecure" impersonation. any modern facility would add step up authentication of some sort.

#### <a name="https://github.com/javedmshah/token-exchange-microservice">Implementation of the OAuth 2.0 token exchange RFC 8693</a>
**groovy** code for the independent research documented here [Token Exchange and Delegation](https://community.forgerock.com/t/token-exchange-and-delegation-using-identity-microservices)

#### <a name="https://github.com/javedmshah/oauth-token-microservices">OAuth 2.0 microservices for tokenized grants</a>
**rego** code for open policy agent.
This repository contains an environment variable-based configuration for the sample Identity Microservices built on Kubernetes. The initial configuration can be used with the public bintray docker repository when deploying the early-access microservices docker images.

Use this repository as a starting point for your own custom configuration using environment variables for sample Identity Microservices. Sequence diagrams are included in this repository. The code is not supported anymore and is only there for sample purposes.

#### <a name="https://github.com/javedmshah/env-vars-consul-microservices">Use environment variables with kubernetes deployments</a>
This repo demonstrates how to build an envconsul container for the ForgeRock Identity Microservices using base images from Bintray. It is required that the starting base images have no entrypoint defined and as such the images tagged BASE-ONLY are used and not the ones tagged 1.0.0-SNAPSHOT. The latter are running jetty containers and therefore cannot be used since we are unable to overlay the envconsul process on to them. The base images are also publicly available.

#### <a name="https://github.com/javedmshah/challengeresponse">challenge reponse in access management</a>
**java** code for implementing challenge response scenarios in openam. Old code, unsupported.

#### <a name="https://github.com/javedmshah/andrews-pitchfork-montecarlo">risk modeling</a>
**c#** code to implement Andrew's pitchfork trading techniques and run monte carlo simulations for minimizing max drawdowns.
