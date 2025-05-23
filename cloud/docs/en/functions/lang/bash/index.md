---
title: Development in Bash at Yandex Cloud Functions. Overview
description: 'With the Cloud Functions service, you can run applications written in Bash. Bash runtime has utilities installed by default - jq, YC CLI, AWS CLI version 2.'
---

# Development in Bash. Overview

With {{ sf-name }}, you can run applications written in [Bash](https://www.gnu.org/software/bash/).

The [Bash runtime environment](../../concepts/runtime/index.md#runtimes) has the following utilities pre-installed:

| Name | Purpose |
| ---- | ---- |
| [jq](https://stedolan.github.io/jq/) | For working with JSON. |
| [YC CLI](../../../cli) | To access the {{ yandex-cloud }} API. |
| [AWS CLI version 2](https://docs.aws.amazon.com/cli/index.html) | For using AWS-compatible services. |

For more information about how to use the SDK, see [Using the SDK](sdk.md).

The runtime environment automatically loads and invokes the specified [request handler script](handler.md) for each request. The request content is passed to the script via the standard input stream, `stdin`.

{{ sf-name }} automatically captures the script's standard output stream, `stdout`, and interprets it as a response to the request. The standard error output stream, `stderr`, is sent to the centralized logging system available in {{ yandex-cloud }}. This system also logs service records about the start and end of each function and any errors that occur during its execution. For more information about the log format, see [{#T}](logging.md).

To learn more about how to write `Bash` scripts, see the [Advanced Bash-Scripting Guide]{% if lang == "ru" %}(https://www.opennet.ru/docs/RUS/bash_scripting_guide/){% endif %}{% if lang == "en" %}(https://tldp.org/LDP/abs/abs-guide.pdf){% endif %}.

