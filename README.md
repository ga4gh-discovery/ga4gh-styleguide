# Style guide and best practices for development of GA4GH specifications [![](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/ga4gh-discovery/ga4gh-styleguide/develop/LICENSE)

The goal of this document is to detail the style guide and best practices for development of GA4GH specifications at the technical level.

We draw from experience developing several mature APIs across a range of GA4GH workstreams (mainly Discovery, Cloud, and Data Use and Researcher Identity), including [Beacon](https://github.com/ga4gh-beacon/specification), [Beacon Network](https://github.com/ga4gh-beacon/beacon-network-specification), [Matchmaker Exchange](https://github.com/ga4gh/mme-apis), [Search](https://github.com/ga4gh-discovery/ga4gh-discovery-search), [service-info](https://github.com/ga4gh-discovery/service-info), [Service Registry](https://github.com/ga4gh-discovery/service-registry), [Workflow Execution Service](https://github.com/ga4gh/workflow-execution-service-schemas), [Data Repository Service](https://github.com/ga4gh/data-repository-service-schemas), [Tool Registry Service](https://github.com/ga4gh/tool-registry-service-schemas), [Task Execution Service](https://github.com/ga4gh/task-execution-schemas), [Consent Codes](https://github.com/ga4gh/ga4gh-consent-policy), [Automatable Discovery and Access Matrix](https://github.com/ga4gh/ADA-M), [legacy Core APIs](https://github.com/ga4gh/ga4gh-schemas), and others.

# Table of Contents

[//]: # (- Format, documentaion, GitFLow, Licence, Contributing, Apache voting, propertyNaming, styleguide hierarchy, URI/URN/ID/contact, Swagger tools, CI validation, commit message convention, github labels)
- [API Type](#api-type)
- [FAQ](#faq)

# API Type

First, you need to decide on the type of your API. People typically consider REST and gRPC. While [there are alid reasons to choose gRPC](https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison?view=aspnetcore-3.0), with performance being the most commonly cited one, we recommend you choose REST.

The main reasons include compatibility (vast majority of GA4GH specifications are REST APIs), ease of understanding (REST is a well-established concept and virtually every developer is familiar with it), ease of use (supporting tooling and libraries are avialable across all technology stacks). Standards only make sense if they're well adopted, and ease of understanding and use are critical in supporting adoption. We've learned this the hard way across a range of older GA4GH products, such as Beacon.


# FAQ

### Is this an official GA4GH style guide I have to follow?

This style guide has not gone through any formal approval process and is not mandatory in any way. Having said that, this style guide reflects what we consider good development practices, which have been validated over the years in the context of several GA4GH products. Consistency and interoperability are important - developers often work on several specifications across a range of workstreams, and GA4GH products live in the same ecosystem, where they need to interoperate. If you're looking to implement your standard in a consistent and interoperable way, please consider this document. For ease of use, we recommend linking to [this README.md](README.md) from the README.md in the repository of your specification.