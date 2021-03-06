

# A look at DataOps by bringing DevOps CI/CD methodology to you DataBricks Workspace using Azure GitHub & DevOps Pipelines.

Suppose your Data team is collaborating in DataBricks notebook(s) and would like the ability to source/peer review these notebook changes and continuously deploy them to specific environment(s). This guide will walk through the steps needed to apply typical DevOps practices in a DataOps scenario. 

And what is DataOps again? 
*From Wiki:* **DataOps** is an automated, process-oriented methodology, used by analytic and data teams, to improve the quality and reduce the cycle time of [data analytics](https://en.wikipedia.org/wiki/Data_analysis "Data analysis"). While DataOps began as a set of best practices, it has now matured to become a new and independent approach to data analytics

Lets walk through the steps needed to perform GitHub Trunk based Development, for Python Notebooks, and leverage Azure DevOps Pipelines for Continuous Integration and Deployment into Azure Databricks. We will be be building a Python Notebook that loads some Dog Breed Data (another Pet Store example I know...) and manipulates it. 

*Note, The objective here is to show how to apply DevOps practices to the peer collaboration of this Notebook and how to efficiently deploy it to a Databricks workspace*

## Step 1
**Stand up a Databricks workspace (if you do not already have one) and configure it**

Head to Azure Portal and Create/Configure a new Databricks Workspace
*Note this is a time consuming process, can take up to an hour to provision this workspace*

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/1.png?raw=true)

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/2.png?raw=true)

Once complete, launch your new workspace and create a compute cluster. 
*Note, selecting the defaults is sufficient for this tutorial!*

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/6.png?raw=true)

From the top right selection your workspace followed by user settings

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/7.png?raw=true)

From User Settings, select the Git Integration Tab.
Now configure the GitHub integration between DataBricks and GitHub, which will allow us to create GitHub branches from Databricks and Commit changes to them.
*Note, you will need a GitHub Personal Access Token, for more information on generating one, visit [creating a personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)*

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/8.png?raw=true)

Lets get a Notbook going in Databricks...
Head to Databarick and select "Import & Export Data"

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/11.png?raw=true)

When prompted select the following file to upload [breeds.csv](https://raw.githubusercontent.com/chtrembl/staticcontent/master/petstoredataops/breeds.csv)
Select "Create Table in Notebook" to generate this new Notebook in your workspace

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/12.png?raw=true)

Select your cluster from the drop down, this will handle our query execution...
Under File, rename this Notebook to something more meaningful and click Rename
![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/13.png?raw=true)

*Note, in the autogenerated Notebook, I made the following change in cell 1, I changed false to true for the following, since our CSV contains Table Header Names: first_row_is_header = "**true**"*

Select Run All and you should see the following

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/14.png?raw=true)

Under workspaces you will see your newly created and renamed Notebook. 

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/15.png?raw=true)

Make a change to your Notebook. Consider this change a new Feature that you will be adding to a GitHub Feature Branch to be merged into the Dev workspace. (Which we will create shortly).  Add a new cell with the following Data Frame query and select Run.

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/16.png?raw=true)

Now from the Top Right (Still in DataBricks) Lets click "Git Not Linked" to get this Notebook versioned in our new Feature Branch. 

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/17.png?raw=true)

Select Link, paste in your GitHub Repo location, and Create a new Feature Branch for your local workspace development efforts. (With Trunk Based Development, Feature Branches are perfect for developers to work off of while the perfect the current feature they are working on) select Create and then select Save.

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/18.png?raw=true)

Now head to GitHub and you will see this new feature branch containing your Notebook. You can continue working in Databricks on your Feature Notebook and/or in you IDE of choice. All changes will be saved/committed to this Feature Branch. 

![enter image description here](https://github.com/chtrembl/staticcontent/blob/master/petstoredataops/19.png?raw=true)
