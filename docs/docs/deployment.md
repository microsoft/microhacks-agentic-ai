# Deployment (Optional)

If you’re running this workshop on your own, you'll need to deploy the workshop resources to your Azure subscription. Follow the instructions to deploy the workshop resources.

## Prerequisites

1. A computer running Windows 11, macOS, or Linux.
1. An Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/){:target="_blank"} before you begin.
1. Install the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli){:target="_blank"}.
1. Install [Powershell 7 (supported on Windows, macOS, and Linux)](https://learn.microsoft.com/powershell/scripting/install/installing-powershell){:target="_blank"}.
1. Install [Python 3.13+](https://www.python.org/downloads/){:target="_blank"}.
1. Install the Git CLI. You can download it from the [Git website](https://git-scm.com/downloads){:target="_blank"}.

## Deploy the Azure Resources

2. Open a terminal window.
3. Clone the workshop repo by running the following command:

    ```bash
    git clone https://github.com/gloveboxes/build-your-first-agent-with-azure-ai-agent-service-lab.git
    ```

4. Navigate to the workshop `infra` folder for the repository you cloned in the previous step.

    ```bash
    cd build-your-first-agent-with-azure-ai-agent-service-lab/infra
    ```

5. Run the deployment script with the following command:

    ```bash
    pwsh deploy.ps1
    ```

6. Follow the prompts to deploy the workshop resources to your Azure subscription.

## Run the workshop

After the deployment is complete, follow the steps in the [Lab Introduction](./introduction-self-guided.md) to run the workshop. 

!!! warning
    Please note that the lab instructions reference the Skillable lab environment username and password. Since you are deploying your own resources, you will need to use your own Azure username and password instead.
