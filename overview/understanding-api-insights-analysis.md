# Understanding the API Insights Analyzers

API Insights runs several analyzers, which score your spec files on several dimensions, based on customizable rulesets. The analyzers are:

* **Adherence to OpenAPI Guidelines** promotes consistency across our APIs and promotes good design practices.
* **Documentation Completeness** means that an API contains descriptions and examples for its components, so that the API can be adopted and used efficiently and effectively.
* **Inclusive language** helps ensure that our terminology is free of offensive or exclusionary language. The tech industry has grappled with biases in technical terminology for decades. API Insights helps you programmaticallyu detect and eliminate biased language in your APIs. The Inclusive Language guidelines included by default detect the use of terms such as *master* and *slave* or *blacklist* and *whitelist*. The analysis report shows some suggested alternatives such as *primary/secondary* and *blocklist/allowlist*.
* **Security** is extremely important for any API. Over 90% of organizations that use APIs had a security incident in the last year.

For more information about each of these analyzers and the rules that they use, see the **References** section.

You can configure API Insights to use your own custom rulesets, or implement any of the following Cisco rulesets:

* [Doc Completeness and REST Guidelines](https://github.com/cisco-developer/api-insights-openapi-rulesets/)
* [Inclusive Language](https://github.com/cisco-open/inclusive-language)

API Insights provides line-by-line breakdowns of your spec files, and assigns severity ratings to any issues that it detects, so you can easily investigate and remediate any problems that it finds. The severity categories that API Insights uses are as follows. These may help you prioritize which items to work on first.

* **Error**: There is a strong industry precedent for implementing this guideline, or a security problem exists due to the identified line in the specification file.
* **Warning**: This guideline is considered a best practice for API design.
* **Info**: This guideline helps your users understand or use your API.
* **Hint**: This guideline might apply in your spec file, so you should review the rule and guidance to determine if changes need to be made.
