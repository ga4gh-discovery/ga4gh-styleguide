# Style guide and best practices for development of GA4GH specifications [![](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/ga4gh-discovery/ga4gh-styleguide/develop/LICENSE)

The goal of this document is to detail the style guide and best practices for development of GA4GH specifications at the technical level.

We draw from experience developing several mature APIs across a range of GA4GH workstreams (mainly Discovery, Cloud, and Data Use and Researcher Identity), including [Beacon](https://github.com/ga4gh-beacon/specification), [Beacon Network](https://github.com/ga4gh-beacon/beacon-network-specification), [Matchmaker Exchange](https://github.com/ga4gh/mme-apis), [Search](https://github.com/ga4gh-discovery/ga4gh-discovery-search), [Service Info](https://github.com/ga4gh-discovery/service-info), [Service Registry](https://github.com/ga4gh-discovery/service-registry), [Workflow Execution Service](https://github.com/ga4gh/workflow-execution-service-schemas), [Data Repository Service](https://github.com/ga4gh/data-repository-service-schemas), [Tool Registry Service](https://github.com/ga4gh/tool-registry-service-schemas), [Task Execution Service](https://github.com/ga4gh/task-execution-schemas), [Consent Codes](https://github.com/ga4gh/ga4gh-consent-policy), [Automatable Discovery and Access Matrix](https://github.com/ga4gh/ADA-M), [legacy Core APIs](https://github.com/ga4gh/ga4gh-schemas), and others.

# Table of Contents

- [Style](#style)
- [Format](#format)
- [File Type](#file-type)
- [File Name](#file-name)
- [Testing](#testing)
- [Repository Setup](#repository-setup)
  - [Hosting](#hosting)
  - [Issues](#issues)
    - [Labels](#labels)
    - [Milestones](#milestones)
- [License](#license)
- [Versioning](#versioning)
- [FAQ](#faq)
- [TODO](#todo)

# Style

**TL;DR: REST.**

First, you need to decide on the style of your API. People typically consider [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) and [gRPC](https://grpc.io/). While [there are alid reasons to choose gRPC](https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison?view=aspnetcore-3.0), with performance being the most commonly cited one, we recommend you choose REST.

The main reasons include:

- Compatibility.

  The vast majority of GA4GH specifications are REST APIs, e.g. [Beacon](https://github.com/ga4gh-beacon/specification), [Beacon Network](https://github.com/ga4gh-beacon/beacon-network-specification), [Service Info](https://github.com/ga4gh-discovery/service-info), [Service Registry](https://github.com/ga4gh-discovery/service-registry), [Workflow Execution Service](https://github.com/ga4gh/workflow-execution-service-schemas), [Data Repository Service](https://github.com/ga4gh/data-repository-service-schemas), [Tool Registry Service](https://github.com/ga4gh/tool-registry-service-schemas), [Task Execution Service](https://github.com/ga4gh/task-execution-schemas).

- Familiarity.

  REST is a well established API style and virtually every developer is familiar with it

- Ease of use.

  Supporting tooling and libraries are available across all technology stacks.

Standards only make sense if they're well adopted, and familiarity and ease of use are critical in supporting developer adoption. We've learned this the hard way across a range of older GA4GH products, such as Beacon.

# Format

**TL;DR: OpenAPI 3.**

There are 4 formats that have been used to specify REST APIs in GA4GH - [OpenAPI](https://swagger.io/specification/), [JSON Schema](https://json-schema.org/), [Protocol Buffers](https://developers.google.com/protocol-buffers/), and [Avro IDL](https://avro.apache.org/docs/1.8.2/idl.html).

Some projects have gone through several of these formats over time. For example, Beacon started with Avro IDL, evolved to Protocol Buffers, and finally landed on OpenAPI. Major reasons for moving away from Avro IDL and Protocol Buffers included the facts that they're not great for specifying REST APIs (dealing with endpoints, requests/responses, and not leveraging the binary format offered by their respective technologies), and are not developer-friendly (steep learning curve, small user base). On top of that, JSON Schema and OpenAPI provide generally better tooling. As such, we advise against using these formats nowadays.

The choice between OpenAPI and JSON Schema comes down to the scope of your specification. JSON Schema is not good for specifying APIs, but excels at specifying data models. In fact, OpenAPI leverages JSON Schema for this reason. If your specification involves endpoints, use OpenAPI. If your specification contains only data models, use JSON Schema. Vast majority of GA4GH specifications use OpenAPI.

Once you decide to use OpenAPI, you have a choice between version 3, and older 2. Majority of GA4GH specifications use version 3, and we recommend you do the same. However, it should be noted that even though OpenAPI 3 was released mid-2017, as of mid-2019, this version of the specification sometimes has only experimental support common tooling (validation, compliance testing etc.). In general, that has not been a big issue for us, but keep the tooling in mind when making the decision.

# OpenAPI

## Basic conventions

## File type

**TL;DR: YAML.**

An OpenAPI document that conforms to the specification is itself a JSON object, which may be represented either in JSON or YAML format. YAML is a superset of JSON, [is generally considered more human-readable](https://www.quora.com/What-situation-would-you-use-YAML-instead-of-JSON-or-XML), and [has good extra features such as commenting, aliasing and anchoring](http://sangsoonam.github.io/2017/03/13/yaml-vs-json.html). We consider readability and commenting very useful when specifying APIs, and recommend using YAML over JSON.

XML [is considered legacy and is not recommended](https://everypageispageone.com/2016/01/28/why-does-xml-suck/).

## File name

**TL;DR: `openapi.yaml`.**

Most likely, your specification is going to consist of a single file. We recommend you name it `openapi.yaml`. This is the common default name, and would allow you to run tools with their default setting.

If your specification consists of multiple files, prefer domain-specific names.

## Testing

**TL;DR: Travis CI with OAS Validator.**

WIth the OAS specification being the main artifact you're delivering, it's important you test it continuously. We recommend setting up a CI solution and trigger builds on pull requests. Travis CI is the most common choice in GA4GH due to its ease of use.

At minimum, you should make sure your specification is valid. Several GA4GH specifications use [OAS Validator](https://github.com/mcupak/oas-validator), we recommend you do the same.

# Repository Setup

## Hosting

**TL;DR: GitHub.**

You should use a _public_ repository on [GitHub](https://github.com).

## Issues

### Labels

**TL;DR: feature, bug, task, wontfix.**

You'll probably need at least 3 kinds of labels: _issue type_, _status_ and _requester_.

For issue types, we recommend starting with 3 basic labels: _feature_ (new feature or request), _bug_ (something isn't working), and _task_ (a task not requiring code changes).

For statuses, we recommend to start with a single _wontfix_ (this will not be worked on), to distinguish between closed issues that were resolved and rejected. Later on, you might choose to add more labels for finer-grained status notation, e.g. _in progress_.

Optionally, you might want to label your issues based on who requested it through various channels, which would typically reflect names of driver projects.

Consistency is good, and developers often contribute to many GA4GH repositories. You should use consistent issue names, descriptions and colour codes. See e.g. [service-info labels](https://github.com/ga4gh-discovery/ga4gh-service-info/labels).

### Milestones

**TL;DR: SemVer releases, 1.0.0.**

Having milestones reflecting releases as per [semantic versioning](https://semver.org) is a good practice. You'll probably want to start with _1.0.0_ as the first major release with backward compatibility commitment, to capture the specification at a point where it will be reviewed by the PRC. To pass product review, you'll need several implementations from the driver projects, who will continuously need a stable version of the specification to develop against. Start with the _0.1_ milestone for your first usable spec and go from there as per semantic versioning.

## License

**TL;DR: Apache 2.0.**

While GA4GH does not prescribe a particular license, practically all our projects use [Apache 2.0](/LICENSE). This will most likely suit your needs.

Include the license text in your repository [like this](LICENSE).

# Versioning

**TL;DR: SemVer.**

[Semantic versioning](https://semver.org) is used across GA4GH. It's a good practice to use 1.0.0 release as the target for PRC approval.

# Tools

Tools you might find useful for your specifications:

- [GA4GH Specification Template](https://github.com/mcupak/ga4gh-specification-template)
- [OAS Validator](https://github.com/mcupak/oas-validator)
- [service-info](https://github.com/ga4gh-discovery/ga4gh-service-info)

# FAQ

### Is this an official GA4GH style guide I have to follow?

This style guide has not gone through any formal approval process and is not mandatory in any way. Having said that, this style guide reflects what we consider good development practices, which have been validated over the years in the context of several GA4GH products. Consistency and interoperability are important - developers often work on several specifications across a range of workstreams, and GA4GH products live in the same ecosystem, where they need to interoperate. If you're looking to implement your standard in a consistent and interoperable way, please consider this document. For ease of use, we recommend linking to [this README.md](README.md) from the README.md in the repository of your specification.

# TODO

- Documentation
- GitFLow
- Contributing rules
- Apache voting
- Property naming
- Styleguide hierarchy
- URI/URN/ID/contact
- Swagger tools
- Badges
- CI validation
- commit message convention
- default repository facets enabled
- repository naming
- API extensions
- Service types and API referral
- Service info
- Error representation
