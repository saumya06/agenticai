---
layout: default
title: Instructor Guide
# permalink: /setupguide/
nav_order: 4
---
# 🏦 Xero Setup and Connection Guide 

## Use Case Description

This lab provides step-by-step instructions for instructors to set up Xero connection and create an app for integration with IBM watsonx Orchestrate. This guide covers the complete process from creating a Xero account to establishing the connection in watsonx Orchestrate and creating an agent with Xero MCP server capabilities.

## Prerequisites

- Access to internet and email
- IBM watsonx Orchestrate access
- Valid email address for Xero account creation

## Step by step instructions to set up Xero Integration:

### Part 1: Xero Account Setup

1. **Create Xero Account**
   - Navigate to [https://www.xero.com](https://www.xero.com)
   - Click on "Start your free trial" or "Sign up"
   - Fill in your details including email, password, and company information
   - Complete the account verification process through email

2. **Change Country Setting to New Zealand**
   - Once logged into your Xero dashboard, click on the company name on top left:
   ![alt text](../imgs/imgs_c/xero-change-country.png)
   - Select **My Xero** from the dropdown
   ![alt text](../imgs/imgs_c/click-my-xero.png)
   - In the new tab that opens, click on change country.
   ![alt text](../imgs/imgs_c/xero-change-country.png)
   - Change the country from the default to **New Zealand**
   ![alt text](../imgs/imgs_c/select%20NZ.png)

### Part 2: Creating Xero App

3. **Access Developer Portal**
   - Navigate to [https://developer.xero.com](https://developer.xero.com)
   - Sign in using your Xero account credentials
   - Click on **My Apps** in the navigation menu

4. **Create New App**
   - Click on **New app** button
   ![alt text](../imgs/imgs_c/click-new-app.png)
   - Fill in the app details:
     - **App name**: Enter a descriptive name (e.g., "Finance Agent Integration")
     - **Company or App URL**: Add the link to your Xero dashboard screen. An example is shown below
     - Choose **Custom conection**
       
     ![alt text](../imgs/imgs_c/fill-app-details.png)

   - Click **Create app**

5. **Configure App Scopes and authenticate app**
   - In the app configuration page, scroll to the **Scopes** section
   - Select the following required 7 scopes:
     - `accounting.transactions`
     - `accounting.contacts`
     - `accounting.settings`
     - `accounting.reports.read`
     - `payroll.settings`
     - `payroll.employees`
     - `payroll.timesheets`
   - Click **Save and Connect** to apply the scope settings, and **Authorization Email Sent** pop-up will appear at bottom-left of screen.
   ![alt text](../imgs/imgs_c/scope-auth-mail-sent.png)

   - Check your email for the authentication email from Xero, and click on connect.
   ![alt text](../imgs/imgs_c/open-email-click-connect.png)
   
   - Review the permissions and click **Allow Access** to authorize the connection
   ![alt text](../imgs/imgs_c/allow-access.png)

7. **Retrieve Credentials**
   - Return to your app page in the Xero Developer Portal. You may have to refresh the Developer Portal page after allowing access.
   - **Generate Secret** by clickin on the button.
   - Note down the following credentials (you'll need these for watsonx Orchestrate):
     - **Client ID**: Copy this value
     - **Client Secret**: Copy this value (click "Show" to reveal)
     ![alt text](../imgs/imgs_c/come-back-apps-secret.png)

### Part 3: Setting up Connection in watsonx Orchestrate
We are doing this so that participants can directly connect to MCP server and tools, and they don't have to go through process of creating a MCP connection. For this we will first create connection details to Xero MCP server, and then connect to this server via a sample agent.

8. **Access watsonx Orchestrate**
   - Log into your IBM watsonx Orchestrate instance
   - Navigate to the **Connections** section from the main menu
   ![alt text](../imgs/imgs_c/connections-tab.png)

9. **Create Xero Connection in WxO**
   - Click on **Add new Connection**
     
   ![alt text](../imgs/imgs_c/add-new-connection.png)

   - Provide the details for the connection - Unique **Connection ID**, name and description, and click save and continue. For example, `xero-connection-mcp-[your initial]`
     
   ![alt text](../imgs/imgs_c/conection-details.png)

   - Select **Authentication type** as **Key Value Pair**, and **Credential type** as **Team credentials**.
     
   ![alt text](../imgs/imgs_c/draft-env-kv-pair-team.png)

   - Provide the required values in the key-value as `XERO_CLIENT_ID` and `XERO_CLIENT_SECRET` that you got earlier, click **Connect** and then **Next**
     
   ![alt text](../imgs/imgs_c/provide-values-click-connect.png)

   - In the next screen, repeat the process for the **Live** environment. The one you did earlier was for **Draft** environment. Finally, click **Add connection**
     
   ![alt text](../imgs/imgs_c/repeat-for-live-env.png)


### Part 4: Creating Agent with Xero MCP Server

10. **Create New Agent**
    
    - Navigate to **Agent Builder** in watsonx Orchestrate
      
     ![alt text](../imgs/imgs_c/agent-builder-tab.png)

    - Click on **Create agent**
      
     ![alt text](../imgs/imgs_c/create-agent.png)

    - Select **'Create from scratch'**, and add agent details
    - Give your agent a unique name (e.g., "[Your Initial]_Xero_Finance_Agent")
    - Add description: "This agent provides comprehensive finance management capabilities through Xero integration, including invoice management, contact management, and financial reporting."
    
    ![alt text](../imgs/imgs_c/provide-agent-details-create.png)

    - Click on **Create**

12. **Add Xero MCP Server**
    - After the agent creation, scroll to the **Toolset** section, click on **Add tool**
    ![alt text](../imgs/imgs_c/agent-launcher-click-tools.png)

    - Select **Add from File or MCP Server**
    ![alt text](../imgs/imgs_c/add-file-mcp-server.png)

    - Click on **Import from MCP Server**
    ![alt text](../imgs/imgs_c/import-from-mcp-server.png)

    - Click on **add MCP server**
    ![alt text](../imgs/imgs_c/add-mcp-server.png)

    - In the next screen, provide MCP server details: unique **Server name**. For example: `xero-mcp-server-workshop-[your initial]` and description.
    - From **Select Connection** dropdown, choose the connection you created earlier.
    - Enter the following **Install command**
      ```bash
      npx -y @xeroapi/xero-mcp-server@latest
      ```
    - Click **Connect**, and then done.
    ![alt text](../imgs/imgs_c/provide-mcp-server-connection-details.png)

    - The next screen will load the list of tools available as part of this MCP server, toggle on the '**list-invoices**' and '**list-contacts**' tools which are required for the later part of the labs.
    ![alt text](../imgs/imgs_c/once-conneceted-see-all-the-tools.png)


## Next Steps
In this guide, we have configured the xero connections in our wxo environment, and users in the following labs can directly search for tools from the MCP server for their use.

## Note
The demo company expires every 30 days. To recreate, login to Xero and create the company again.
Then go to the app connection in Xero developer. You will see the app is disconnected, connect it again.

