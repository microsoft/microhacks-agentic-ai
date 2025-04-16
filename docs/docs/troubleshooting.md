## Assign an Azure Resource Group User Role

You may need to assign a user role to the resource group that contains the Azure AI Agents Service. This role allows the agent app to access the Azure AI Agents Service and models.

Follow these steps to assign a user role to the resource group:

1. Open a terminal window. The terminal app is **pinned** to the Windows 11 taskbar.

    ![Open the terminal window](./media/windows-taskbar.png){ width="300" }

1. Run the following command to authenticate with Azure:

    ```powershell
    az login
    ```

    !!! note
        You'll be prompted to open a browser link and log in to your Azure account.

        1. A browser window will open automatically, select **Work or school account** and click **Next**.

        1. Use the **Username** and **Password** found in the top section of the **Resources** tab in the lab environment.

        1. Select **OK**, then **Done**.

1. Then select the **Default** subscription from the command line.

1. Once you've logged in, run the following command to assign the **user** role to the resource group:

    ```powershell
    $subId = $(az account show --query id --output tsv) `
    ;$objectId = $(az ad signed-in-user show --query id -o tsv) `
    ; az role assignment create --role "f6c7c914-8db3-469d-8ca1-694a8f32e121" --assignee-object-id $objectId --scope /subscriptions/$subId/resourceGroups/"rg-agent-workshop" --assignee-principal-type 'User'
    ```

1. Leave the terminal window open for the next steps.
