## Introduction

Grounding conversations with Bing is one of several tools provided by the Azure AI Agent Service. Grounding with Bing allows your app to search for information relevant to the conversation. For example, you might want to search for competitive product information.

## Lab Exercise

In this lab, you'll enable Bing Grounding to provide competitive sales analysis of Contoso products and categories.

## Create a with Grounding with Bing Search resource

You'll need to create a **Grounding with Bing Search Service** resource in the Azure portal and connect it to the Azure AI Foundry portal.

Follow these steps to create a Grounding with Bing Search Resource:

1. [Click to create a Grounding with Bing Search Resource](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/GalleryItemDetailsBladeNopdl/id/Microsoft.BingGroundingSearch){:target="_blank"}.

    !!! Note
        You may need to sign in to your Azure account and or clear the welcome screen to access the Azure portal.

1. Select **Create**.
1. Select the **rg-agent-workshop** resource group from the drop-down list.
1. Name the resource as follows:

    ```text
    groundingwithbingsearch
    ```

1. Select the **Grounding with Bing Search** pricing tier.
1. Confirm **I confirm I have read and understood the notice above**.
1. Select **Review + create**.
1. Select **Create**.
1. Wait for deployment to complete, then click **Go to resource**.
1. Select **Overview** from the side-bar menu.
1. Select the **Go to Azure AI Foundry Portal** button.
<!-- 1. Select **Sign in** and enter your Azure account credentials. -->

## Create a Bing Search Connection in AI Foundry

Next, we will create a Bing Search connection in the Azure AI Foundry portal. This connection enables the agent app to access the Bing Search service using the agent **Grounding-with-Bing-Search**.

To create a Bing Search connection in the Azure AI Foundry portal, follow these steps:

1. Verify that your project "Agent-Service-Workshop" is selected.
1. From the sidebar menu, click the **Management Center** button. The button is pinned at the **bottom** of the sidebar.
1. From the side-bar menu, select **Connected resources**.
1. Click **+ New Connection**.
1. Scroll to the Knowledge section and select "Grounding with Bing Search"
1. Click the **Add connection** button to the right of your `groundingwithbingsearch` resource.
1. Click **Close**

For more information, visit the [Grounding with Bing Search](https://learn.microsoft.com/en-us/azure/ai-services/agents/how-to/tools/bing-grounding){:target="_blank"} documentation.

### Enable Grounding with Bing Search in the Agent App

1. Open the file `main.py`.

1. **Uncomment** the following lines by removing the **"# "** characters

    ```python
    # INSTRUCTIONS_FILE = "instructions/instructions_bing_grounding.txt"
    
    # bing_connection = project_client.connections.get(connection_name=BING_CONNECTION_NAME)
    # bing_grounding = BingGroundingTool(bing_connection)
    # toolset.add(bing_grounding)
    ```

    !!! warning
        The lines to be uncommented are not adjacent. When removing the # character, ensure you also delete the space that follows it.

1. Review the code in the `main.py` file.

    After uncommenting, your code should look like this:

    ``` python
    INSTRUCTIONS_FILE = "instructions/instructions_function_calling.txt"
    INSTRUCTIONS_FILE = "instructions/instructions_code_interpreter.txt"
    INSTRUCTIONS_FILE = "instructions/instructions_file_search.txt"
    INSTRUCTIONS_FILE = "instructions/instructions_bing_grounding.txt"


    async def add_agent_tools():
        """Add tools for the agent."""

        # Add the functions tool
        toolset.add(functions)

        # Add the code interpreter tool
        code_interpreter = CodeInterpreterTool()
        toolset.add(code_interpreter)

        # Add the tents data sheet to a new vector data store
        vector_store = await utilities.create_vector_store(
            project_client,
            files=[TENTS_DATA_SHEET_FILE],
            vector_name_name="Contoso Product Information Vector Store",
        )
        file_search_tool = FileSearchTool(vector_store_ids=[vector_store.id])
        toolset.add(file_search_tool)

        # Add the Bing grounding tool
        bing_connection = await project_client.connections.get(connection_name=BING_CONNECTION_NAME)
        bing_grounding = BingGroundingTool(connection_id=bing_connection.id)
        toolset.add(bing_grounding)
    ```

### Review the Instructions

The **instructions/instructions_bing_grounding.txt** adds a new tool, "Competitive Insights for Products and Categories" that instructs the agent to use Bing Search to:

- Gather competitive product names, company names, and prices
- Never answer questions that are not related to outdoors camping and sports gear
- Make sure the search results are concise and directly relevant to the query

This ensures that queries remain relevant to Contoso and maintain a focus on contextually appropriate searches.

### Run the Agent App

First, launch the app from the terminal as before:

1. Press <kbd>F5</kbd> to run the app.

This time, let's run our completed app in the Agents Playground within Azure AI Foundry:

1. In Azure AI Foundry, click "Agents" in the left hand nav
1. Select your AI Foundtry project
2. Select your agent: "Contoso Sales Agent"
3. In the right pane, click "Try in Playground".

    !!! tip
        You may need to click the "Refresh" button on the "Create and debug your agents" page if you already had it open.

You will see a chat window with a field at the bottom where you can enter your queries.

### Start a Conversation with the Agent

The agent combines data from the Contoso sales database, the Tents Data Sheet, and Bing Search to provide comprehensive responses, so the results will vary depending on the query.

1. **What beginner tents do we sell?**

    !!! info
        This information mainly comes from the file we provided in the vector information store. 

2. **What beginner tents do our competitors sell? Include prices.**

    !!! info
        This information comes from the internet, and includes real-world product names and prices.

3. **Show as a bar chart**

    !!! info
        AI Agent Service is again using Code Interpreter to create the chart, but this time with
        real-world data sourced in the previous query. As before, look in `src/workshop/files` to view the chart.

4. **Show the tents we sell by region that are a similar price to our competitors beginner tents.**

    !!! info
        This query relies on the reasoning capabilities of the underlying large language model, along with the data returned by function calling. 

5. **Download the data as a human-readable JSON file**

    !!! info
        This query again relies on Code Interpreter to create the file from the context in the 
        previous queries.
    

