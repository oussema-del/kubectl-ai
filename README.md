# kubectl-ai

kubectl-ai is an AI powered kubernetes agent that runs in your terminal.

![kubectl-ai demo GIF using: kubectl-ai "how's nginx app doing in my cluster"](./.github/kubectl-ai.gif)

## Quick Start

First, ensure that kubectl is installed and configured.

### Installation

1. Download the latest release from the [releases page](https://github.com/GoogleCloudPlatform/kubectl-ai/releases/latest) for your target machine.

2. Untar the binary, make it executable and move it to a directory included in your $PATH (as shown below).

```shell
$ tar -zxvf kubectl-ai_Darwin_arm64.tar.gz
$ chmod a+x kubectl-ai
$ sudo mv kubectl-ai /usr/local/bin/
```

### Invoking

Set your Gemini API key as an environment variable. If you don't have a key, get one from [Google AI Studio](https://aistudio.google.com).

```bash
export GEMINI_API_KEY=your_api_key_here
```

Run interactively:

```shell
kubectl-ai
```

The interactive mode allows you to have a chat with `kubectl-ai`, asking multiple questions in sequence while maintaining context from previous interactions. Simply type your queries and press Enter to receive responses. To exit the interactive shell, type `exit` or press Ctrl+C.

Or, run with a task as input:

```shell
kubectl-ai -quiet "fetch logs for nginx app in hello namespace"
```

Combine it with other unix commands:

```shell
kubectl-ai < query.txt
# OR
echo "list pods in the default namespace" | kubectl-ai
```

You can even combine a positional argument with stdin input. The positional argument will be used as a prefix to the stdin content:

```shell
cat error.log | kubectl-ai "explain the error"
```

## Extras

You can use the following special keywords for specific actions:

* `model`: Display the currently selected model.
* `models`: List all available models.
* `version`: Display the `kubectl-ai` version.
* `reset`: Clear the conversational context.
* `clear`: Clear the terminal screen.
* `exit` or `quit`: Terminate the interactive shell (Ctrl+C also works).

### Invoking as kubectl plugin

Use it via the `kubectl` plug interface like this: `kubectl ai`.  kubectl will find `kubectl-ai` as long as it's in your PATH.  For more information about plugins please see: https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/


### Examples

```bash
# Get information about pods in the default namespace
kubectl-ai -quiet "show me all pods in the default namespace"

# Create a new deployment
kubectl-ai -quiet "create a deployment named nginx with 3 replicas using the nginx:latest image"

# Troubleshoot issues
kubectl-ai -quiet "double the capacity for the nginx app"
```

The `kubectl-ai` will process your query, execute the appropriate kubectl commands, and provide you with the results and explanations.

## k8s-bench

kubectl-ai project includes [k8s-bench](./k8s-bench/README.md) - a benchmark to evaluate performance of different LLM models on kubernetes related tasks. Here is a summary from our last run:

| Model | Success | Fail |
|-------|---------|------|
| gemini-2.5-flash-preview-04-17 | 10 | 0 |
| gemini-2.5-pro-preview-03-25 | 10 | 0 |
| gemma-3-27b-it | 8 | 2 |
| **Total** | 28 | 2 |

See [full report](./k8s-bench.md) for more details.

---

*Note: This is not an officially supported Google product. This project is not
eligible for the [Google Open Source Software Vulnerability Rewards
Program](https://bughunters.google.com/open-source-security).*

# Oussema-Bouarada
🚀 Senior DevOps Engineer | AWS • Azure • Kubernetes Certified | CI/CD & SRE | Infrastructure Automation Enthusiast
