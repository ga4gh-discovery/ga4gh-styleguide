# Style guide and best practices for development of GA4GH specifications [![](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/ga4gh-discovery/ga4gh-styleguide/develop/LICENSE)

The goal of this document is to detail the style guide and best practices for development of GA4GH specifications at the technical level.

We draw from experience developing several mature APIs across a range of GA4GH workstreams (mainly Discovery, Cloud, and Data Use and Researcher Identity), including [Beacon](https://github.com/ga4gh-beacon/specification), [Beacon Network](https://github.com/ga4gh-beacon/beacon-network-specification), [Matchmaker Exchange](https://github.com/ga4gh/mme-apis), [Search](https://github.com/ga4gh-discovery/ga4gh-discovery-search), [Service Info](https://github.com/ga4gh-discovery/service-info), [Service Registry](https://github.com/ga4gh-discovery/service-registry), [Workflow Execution Service](https://github.com/ga4gh/workflow-execution-service-schemas), [Data Repository Service](https://github.com/ga4gh/data-repository-service-schemas), [Tool Registry Service](https://github.com/ga4gh/tool-registry-service-schemas), [Task Execution Service](https://github.com/ga4gh/task-execution-schemas), [Consent Codes](https://github.com/ga4gh/ga4gh-consent-policy), [Automatable Discovery and Access Matrix](https://github.com/ga4gh/ADA-M), [legacy Core APIs](https://github.com/ga4gh/ga4gh-schemas), and others.

# Table of Contents

[//]: # (- documentation, GitFLow, License, Contributing, Apache voting, propertyNaming, styleguide hierarchy, URI/URN/ID/contact, Swagger tools, CI validation, commit message convention, github labels)
- [Style](#style)
- [Format](#format)
- [File Type](#file-type)
- [File Name](#file-name)
- [License](#license)
- [FAQ](#faq)

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

# File type

**TL;DR: YAML.**

An OpenAPI document that conforms to the specification is itself a JSON object, which may be represented either in JSON or YAML format. YAML is a superset of JSON, [is generally considered more human-readable](https://www.quora.com/What-situation-would-you-use-YAML-instead-of-JSON-or-XML), and [has good extra features such as commenting, aliasing and anchoring](http://sangsoonam.github.io/2017/03/13/yaml-vs-json.html). We consider readability and commenting very useful when specifying APIs, and recommend using YAML over JSON.

XML [is considered legacy and is not recommended](https://everypageispageone.com/2016/01/28/why-does-xml-suck/).

# File name

**TL;DR: `openapi.yaml`.**

Most likely, your specification is going to consist of a single file. We recommend you name it `openapi.yaml`. This is the common default name, and would allow you to run tools with their default setting.

If your specification consists of multiple files, prefer domain-specific names.

# License

**TL;DR: Apache 2.0.**

While GA4GH does not prescribe a particular license, practically all our projects use [Apache 2.0](/LICENSE). This will most likely suit your needs.

Include the license text in your repository [like this](LICENSE).

# FAQ

### Is this an official GA4GH style guide I have to follow?

This style guide has not gone through any formal approval process and is not mandatory in any way. Having said that, this style guide reflects what we consider good development practices, which have been validated over the years in the context of several GA4GH products. Consistency and interoperability are important - developers often work on several specifications across a range of workstreams, and GA4GH products live in the same ecosystem, where they need to interoperate. If you're looking to implement your standard in a consistent and interoperable way, please consider this document. For ease of use, we recommend linking to [this README.md](README.md) from the README.md in the repository of your specification.