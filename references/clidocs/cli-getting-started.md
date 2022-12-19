## API Insights CLI (api-insights-cli) Overview

The `api-insights-cli` command-line utility allows you to analyze, score, and upload spec files to the API Insights service, all from your local environment. Although the local CLI utility can interact with the API Insights service and interface with Git repositories, you do not need a service or repository in order to use many of the CLI features.

## Prerequisites

Before you begin setting up the API Insights CLI, do the following:

* If you are running API Insights locally using a Helm chart, run the following command to expose the API Insights API at `http://localhost:8081/v1/apiregistry`:

  ```shell
  kubectl -n api-insights port-forward svc/api-insights 8081:80
  ```

* Author or download a spec file to your local environment. If you do not have a local spec file on hand, you can download a sample pet store OpenAPI 3 spec file by running the following command:

  ```shell
  wget https://raw.githubusercontent.com/OAI/OpenAPI-Specification/main/examples/v3.0/petstore.json
  ```

## Setting Up the API Insights CLI

### Setting Up the CLI on Windows

To run the CLI on Windows, download the `api-insights-cli` utility for Windows and your specific architecturefrom [Cisco DevNet](https://github.com/cisco-developer/api-insights/releases). Then add the file's location to your PATH variable and run it from the command line as `api-insights-cli`.

### Setting Up the CLI on MacOS

To run the CLI on Mac, download the `api-insights-cli` utility for MacOS and your specific architecture from [Cisco DevNet](https://github.com/cisco-developer/api-insights/releases), then do the following:

1. Change the file's permissions by running `chmod a+x [path to file]` where [path to file] is the path to the `api-insights-cli` file, including the filename.
1. Add the file to your PATH variable. In MacOS versions before 10.15 (Catalina), your PATH variable is stored in either `.bashrc` or `.bash_profile`. In version 10.15 and later, the PATH variable is stored in `.zshrc` or `.zsh_profile`.
1. Run the CLI from the command line as `api-insights-cli`.
>> Note Depending on you laptop's security setting, you may need to run ```xattr -d com.apple.quarantine api-insights-cli``` this command to allow new downloaded binary to be executed. 
   

## How to Analyze a Local Spec File

To run all of the API Insights analyzers on a local spec file, run the following:

```shell
`api-insights-cli analyze [filepath]`
```

To run only a specific analyzer on a local spec file, add the flag `--analyzer` followed by one of the following. Note that in order to use `drift`, you must configure APIClarity.

* `guidelines`
* `completeness`
* `inclusive-language`
* `drift`

API Insights returns the analysis report as output in your console. The final score summary at the end of the report looks like the following:

```shell
  #  SEVERITY  CODE  FINDINGS  RECOMMENDATION  AFFECTED ITEMS
0 Findings (0 Error, 0 Warning, 0 Info, 0 Hint)

  # |      ANALYZER      | SCORE | ERROR | WARNING | INFO | HINT
----+--------------------+-------+-------+---------+------+-------
  2 | Completeness       |    80 |     2 |       0 |    0 |    0
  3 | Drift              |   100 |     0 |       0 |    0 |    0
  4 | REST Guidelines    |    93 |     6 |       4 |    1 |    1
  5 | Inclusive Language |   100 |     0 |       0 |    0 |    0

API Score: 90
```

By default, a spec file fails an analysis on a score of **0**. To configure the score that should be considered "failing", add the tag `--fail-below-score`, followed by the desired cutoff score value as an integer.

## How to Compare Two OAS Spec Files

If you have set up an API Insights remote service and uploaded at least one API spec to it, you can use the API Insights CLI to compare a local version of that spec file to one of the versions on the remote service.

* To compare a local spec file to the **latest version** that is currently on the remote service, run the following:

  ```shell
  api-insights-cli diff LOCAL_SPEC -s REMOTE_SERVICE_ID --latest
  ```

* To compare a local spec file to a **specific version** of the spec file on the remote service, run the following:

  ```shell
  apregistryctl diff LOCAL_SPEC -s REMOTE_SERVICE_ID --version VERSION_STRING
  ```

* To compare a local spec file to a **specific version and revision** of the spec file on the remote service, run the following:

  ```shell
  api-insights-cli diff LOCAL_SPEC -s REMOTE_SERVICE_ID --version VERSION_STRING --revision REVISION_STRING
  ```

To set any of these diff analyses to fail if they detect changes that break backwards compatibility, add the **--fail-on-incompatible** flag to any of these commands.

### SEE ALSO

* [api-insights-cli analyze](api-insights-cli_analyze.md)	 - Analyze local API spec
* [api-insights-cli analyzer](api-insights-cli_analyzer.md)	 - Manage analyzers
* [api-insights-cli analyzer-rule](api-insights-cli_analyzer-rule.md)	 - Manage analyzer rules
* [api-insights-cli diff](api-insights-cli_diff.md)	 - Diff local and remote API specs
* [api-insights-cli service](api-insights-cli_service.md)	 - Manage services and related specs
* [api-insights-cli spec](api-insights-cli_spec.md)	 - Manage specs
* [api-insights-cli spec-analysis](api-insights-cli_spec-analysis.md)	 - Manage spec analyses

###### Auto generated by spf13/cobra on 19-Aug-2022
