# Databricks-Connect Container

This container is designed for developing PySpark application in VS Code using Databricks-Connect. Databricks VSCode extension can be used alongside to sync your workspace. Technically it should work for Scala, Java & R - though I haven't tried.

It can be used as a Docker Container or as a cloud hosted container using  [CodeSpaces](https://visualstudio.microsoft.com/services/visual-studio-codespaces/).

## Requirements

### Mac OS
* VS Code with:
	* [Remote Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
	* [Databricks VSCode Extension](https://marketplace.visualstudio.com/items?itemName=paiqo.databricks-vscode)
	* [Visual Studio IntelliCode](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)
* Docker Desktop or a [CodeSpace](https://visualstudio.microsoft.com/services/visual-studio-codespaces/) Plan

### Windows 10
* VS Code with:
	* [Remote Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
	* [Databricks VSCode Extension](https://marketplace.visualstudio.com/items?itemName=paiqo.databricks-vscode)
	* [Visual Studio IntelliCode](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)
* Docker or a [CodeSpace](https://visualstudio.microsoft.com/services/visual-studio-codespaces/) Plan
* If using Docker:
  * WSL or [WSL2](https://devblogs.microsoft.com/commandline/announcing-wsl-2/) (WSL2 Preferred)

### Alternative
For a more advanced option you can use any OS and a [Remote Docker Host](https://code.visualstudio.com/docs/remote/containers-advanced#_developing-inside-a-container-on-a-remote-docker-host).

This maybe useful if you cannot run local containers and do not want to use a cloud container. 

## Getting Started

* Set these enviroment variables in a terminal before launching VS Code. Refer to [this guide](https://docs.microsoft.com/en-gb/azure/databricks/dev-tools/databricks-connect#step-2-configure-connection-properties) to locate the connection properties below.

```shell
export DATABRICKS_ADDRESS=<YOUR_DATABRICKS_URL>
export DATABRICKS_API_TOKEN=<YOUR_DATABRICKS_API_TOKEN>
export DATABRICKS_CLUSTER_ID=<YOUR_DATABRICKS_CLUSTER_ID>
export DATABRICKS_ORG_ID=<YOUR_DATABRICKS_ORG_ID>
export DATABRICKS_PORT=<YOUR_DATABRICKS_PORT>
```

**IMPORTANT: Correct the Databricks Connect version in `devcontainer.json` to match Databricks Runtime your cluster is running. Changing any setting in the devcontainer.json after the container has been build requires you to rebuild the container for it take effect**

To open using Docker locally:
* Click on the Green icon in the bottom left of VSCode and select "Reopen in Container"

To open in a CodeSpace:
* Commit your folder to a repo first
* Open the Remote Explorer (left hand toolbar)
* Ensure CodeSpaces is selected in the top drop down
* Click + (Create new CodeSpace)
* Follow the prompts

Set up and configure the [Databricks VSCode Extension](https://marketplace.visualstudio.com/items?itemName=paiqo.databricks-vscode) using instructions in the `Setup and Configuration (VSCode Connection Manager)` section.

## Test it out

### Test Databricks connection
First from command prompt check that you databricks connect install can connect:

```shell
databricks-connect test
```

### Run some Python code
To run python code create a test.py file and paste this code:
```python
from pyspark.sql import SparkSession
spark = SparkSession\
.builder\
.getOrCreate()

print("Testing simple count")

# The Spark code will execute on the Azure Databricks cluster.
print(spark.range(100).count())
```

Press F5 and select the Python debugger.

### Run a Jupyter notebook 
Navigate to the Databricks VSCode extension and navigate to the `Workspace` to find a notebook to open. Double-click the notebook you'd like to open in the editor.

**NOTE: A notebook may display in JSON format. If this happens right click on the tab at the top with the name of the file, select `Reopen Editor With...` and click on `Jupyter Notebook`**

Before running a cell, on the top right corner click on `Select Kernel` and select `Python 3.x.x 64-bit ('dbconnect': conda). Note the Python version maybe different depending on what Databricks Runtime is being used.

Run a cell to execute your code Databricks cluster. VSCode may ask you to install ipykernel - accept the prompt if it does.

## Why?
Because setting up Databricks-Connect (particulary on Windows is a PIA). This allow:
* A common setup between team members
* Better development enviroment
* Multiple side by side versions
* Ability to reset your environment
* Even run the whole thing from a [browser](https://docs.microsoft.com/en-gb/visualstudio/online/how-to/browser)!

### More Information
About VSCode and Containers: https://code.visualstudio.com/docs/remote/containers
