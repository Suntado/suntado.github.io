<a id="top"></a>
# Working with the SuiteCloud CLI

This page assumes you've already completed [Setting up your development environment](/getting-started/setting-up-your-environment.md). You should have all the prerequisite software needed, and be ready to start using the CLI.

<hr />

<a id="what-is-cli"></a>
## What is the SuiteCloud CLI?

The SuiteCloud CLI is a command-line interface provided by NetSuite that allows developers to interact with the SuiteCloud Development Framework (SDF). It enables streamlined management of account customization projects, including importing and deploying custom objects, scripting, and configurations directly to and from a NetSuite account. Designed for automation and integration into modern development workflows, the CLI supports version control, continuous integration, and efficient collaboration across teams.

> For more information regarding SuiteCloud CLI, refer to the [SuiteCloud Docs](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/chapter_1558708800.html).

<hr />

<a id="suitecloud-command"></a>
## The suitecloud command

to use the SuiteCloud CLI, we use the suitecloud command:

<xmp>
suitecloud <command> <options>
</xmp>

<hr />

To see a list of all the commands in SuiteCloud CLI, use suitecloud by itself:

<xmp>
suitecloud
</xmp>

This will list all the commands off in the terminal, and show you how to use them:

<xmp class="terminal-window">
SuiteCloud CLI for Node.js (NetSuite 2025.1)
Usage: suitecloud command [option]
Options:
--version Outputs the version number.
-i, --interactive Runs the command in interactive mode.
-h, --help Displays help for the command.
Commands:
account:manageauth [options] Manages authentication IDs for all your projects. An authentication ID is a custom alias you give to a specific account-role combination.
account:setup [options] Sets up an account to use with SuiteCloud SDK and configures the default auth ID for the SuiteCloud project. This command requires browser-based login to NetSuite.
account:setup:ci [options] Sets up an account to use with SuiteCloud SDK and configures the default auth ID for the SuiteCloud project. This command does not require browser-based login to NetSuite.
To change the default auth ID for the project, run: suitecloud account:setup.
file:create [options] Creates a SuiteScript file.
file:import [options] Imports files from an account to your account customization project. You cannot import files from a SuiteApp.
file:list [options] Lists the files in the File Cabinet of your account.
file:upload [options] Uploads files from your project to an account.
object:import [options] Imports custom objects from your NetSuite account to the SuiteCloud project. In account customization projects (ACP), if SuiteScript files are referenced in the custom objects you import, these files get imported by default.
object:list [options] Lists the custom objects deployed in an account.
object:update [options] Overwrites the custom objects in the project with the custom objects in an account.
project:adddependencies Adds the missing dependencies to the manifest file.
project:create [options] Creates a SuiteCloud project, either a SuiteApp or an account customization project (ACP).
project:deploy [options] Deploys the folder containing the project. The project folder is zipped before deployment, only including the files and folders referenced in the deploy.xml file.
project:package [options] Generates a ZIP file from your project, respecting the structure specified in the deploy.xml file.
project:validate [options] Validates the folder containing the SuiteCloud project.
help [command] Displays help for the command.
</xmp>

<hr />

<a id="help"></a>
## Help

To see specific help pertaining to each individual command, use the --help option:

<xmp>
suitecloud file:upload --help
</xmp>

<xmp class="terminal-window">
suitecloud file:import --help
Usage: suitecloud file:import [options]
Imports files from an account to your account customization project. You cannot import files from a SuiteApp.
Options:
  --calledfromcomparefiles  Message displayed should be different if called from Compare Files.
  --calledfromupdate        Message displayed should be different if called from Update File.
  --excludeproperties       Excludes all file properties within the .attributes folder.
  -i, --interactive         Runs the file:import command in interactive mode.
  --paths <arguments...>    Specifies the File Cabinet paths of the files to import. For example, "/SuiteScripts/file.js".
  -h, --help                Displays help for the command.
</xmp>

<hr />

<a id="project"></a>
## Setting up a project

setting up a suitecloud project is simple and easy. Using the terminal, navigate to the directory you want your project to be located, and use the <strong>suitecloud project:create -i</strong> command.

<xmp>suitecloud project:create -i</xmp>

This will interactively guide you through suitecloud project creation, ending with a fresh project file structure for you to work with.

<xmp class="terminal-window">
suitecloud project:create -i
? Select the project type you want to create. (Use arrow keys)
❯ Account Customization Project 
  SuiteApp 
</xmp>

For the most part, we will almost always be using Account Customization Project type. Refer to the SDF docs for more info regarding the different project types.

<xmp class="terminal-window">
? Select the project type you want to create. Account Customization Project
? Enter the project name.
</xmp>

<xmp class="terminal-window">
? Select the project type you want to create. Account Customization Project
? Enter the project name. test_project_name
? Do you want to include unit testing with the Jest testing framework? ***This will install NPM module dependencies. 
  Yes 
❯ No
</xmp>

> NOTE: In the future, we may perform unit testing with Jest, but for now, select no.

<xmp class="terminal-window">
? Select the project type you want to create. Account Customization Project
? Enter the project name. test_project_name
? Do you want to include unit testing with the Jest testing framework? ***This will install NPM module dependencies. No
Creating the project structure...
The test_project_name project was created successfully.
Navigate to /Users/Andrew/Workspace/test_project_name and run "suitecloud account:setup" to link your project with your account.
Non-interactive execution:
suitecloud project:create --type ACCOUNTCUSTOMIZATION --projectname test_project_name
</xmp>

Now, we navigate to the project folder and run <strong>suitecloud account:setup</strong> to link the project to our NetSuite Account.

> NOTE: when performing the OAuth2 link, you will be prompted to Create a new authentication ID. If you don't have a previously configured auth ID, go through with this step. If you do have previously configured ID's, you are given the option to select one in this propt. Usually we will only have 2 auth id's available for use. One leading to the sandbox, and one leading to production.

If you're already in an existing project, and you need to push files to production after following proper CLI usage, you can switch auth accounts from sandbox to production, and then perform your file:upload command.

<xmp class="terminal-window">
? Select or create an authentication ID (a custom alias you give to a specific account-role combination):
  ***The authentication ID that you select or create will be set up as default. (Use arrow keys)
❯ Create a new authentication ID. 
  ──────────────
  Select a configured authentication ID:
  sdf-sandbox | Suntado LLC [Administrator] | 9090450-sb1.app.netsuite.com 
  ──────────────
</xmp>

<xmp class="terminal-window">
? Select or create an authentication ID (a custom alias you give to a specific account-role combination):
  ***The authentication ID that you select or create will be set up as default. sdf-sandbox | Suntado LLC [Administrator] | 
9090450-sb1.app.netsuite.com
This project will use the authentication ID "sdf-sandbox" as default for the following company and role: Suntado LLC [Administrator]. If you want to change your default credentials, run "suitecloud account:setup" again.
The account has been successfully set up.
</xmp>

After properly authenticating, you should be able to access NetSuite through the CLI!

<hr />

<a id="interactive"></a>
## Interactive

The interactive option inside the cli actually gives us more options and flexibilty when interacting with NetSuite. For example: normally when using the suitecloud file:upload command. If you don't specify interactive, by default the command looks for a path to a file:

<xmp class="terminal-window">
suitecloud file:upload
The authorization credentials associated with sdf-sandbox auhtid are no longer valid. Starting the browser-based authentication for refreshing them.
Authorization refresh completed.
There are validation errors:
"paths" option is mandatory.
You can use the interactive mode by running "suitecloud file:upload -i"
</xmp>

> NOTE: In the future, we may need to curate a set of commands that manually controls which files get uploaded, but for now, -i (interactive) is the best way to upload files to the File Cabinet.

Using interactive mode allows us to upload multiple files at once from a specified directory inside your project folder, getting rid of the need to manually write out file paths:

<xmp class="terminal-window">
suitecloud file:upload -i
? Select folder from where you want to upload files to the File Cabinet. (Use arrow keys)
❯ /SuiteScripts 
  /SuiteScripts/Suntado 
  /SuiteScripts/Suntado/suitelets 
  /SuiteScripts/Suntado/vue-spa 
  /SuiteScripts/Suntado/vue-spa/dist 
  /SuiteScripts/Suntado/vue-spa/dist/assets 
  - /Templates (Restricted Folder)
(Move up and down to reveal more choices)
</xmp>

<xmp class="terminal-window">
? Select the files you want to upload to the File Cabinet. (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed)
❯◯ /SuiteScripts/Suntado/suitelets/vue_spa_suitelet.js
 ◯ /SuiteScripts/Suntado/vue-spa/dist/assets/index-CaecrJKp.js
 ◯ /SuiteScripts/Suntado/vue-spa/dist/assets/index-GOxYMXNJ.css
 ◯ /SuiteScripts/Suntado/vue-spa/dist/index.html
 ◯ /SuiteScripts/Suntado/vue-spa/dist/vite.svg
 
 ? Select the files you want to upload to the File Cabinet. (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed)
 ◉ /SuiteScripts/Suntado/suitelets/vue_spa_suitelet.js
 ◉ /SuiteScripts/Suntado/vue-spa/dist/assets/index-CaecrJKp.js
❯◉ /SuiteScripts/Suntado/vue-spa/dist/assets/index-GOxYMXNJ.css
 ◯ /SuiteScripts/Suntado/vue-spa/dist/index.html
 ◯ /SuiteScripts/Suntado/vue-spa/dist/vite.svg
 </xmp>

 <xmp class="terminal-window">
 ? The selected files will be overwritten in the File Cabinet. Do you want to continue? (Use arrow keys)
❯ Yes 
  No 
 </xmp>

 > NOTE: It is important to note, any files uploaded <strong>WILL</strong> overwrite any existing script in the file cabinet. But, the nice part of this functionality, is there is no new script deployment to perform inside NetSuite after the fact. NetSuite will automatically begin serving whatever the latest script with that name is inside the file cabinet.

 <xmp class="terminal-window">
 ? The selected files will be overwritten in the File Cabinet. Do you want to continue? Yes
/ Uploading files...
 The following files were uploaded:
/SuiteScripts/Suntado/suitelets/vue_spa_suitelet.js
/SuiteScripts/Suntado/vue-spa/dist/assets/index-CaecrJKp.js
/SuiteScripts/Suntado/vue-spa/dist/assets/index-GOxYMXNJ.css
Non-interactive execution:
suitecloud file:upload --paths "/SuiteScripts/Suntado/suitelets/vue_spa_suitelet.js" "/SuiteScripts/Suntado/vue-spa/dist/assets/index-CaecrJKp.js" "/SuiteScripts/Suntado/vue-spa/dist/assets/index-GOxYMXNJ.css"
 </xmp>

> NOTE: Using the command <strong>suitecloud file:import -i</strong> replicates this process, but in reverse. It is always important to remember that importing or uploading files overwrites their remote or local counterparts. 

<hr />

<a id="proper-usage"></a>
## Proper CLI Usage

With the previous section in mind, it is important to know the proper method of using the CLI. We don't want to cause irreversable damage to project files that might be contained inside the FileCabinet, or lose project data because we were careless and used the wrong CLI command. 

<h4>1. Always check out a new working branch inside git when interacting with the CLI</h4>

Checking a new branch out in git, keeps the master branch intact. If something goes wrong and breaks, it's always easy to commit your broken changes to your checked out branch, switch back to master, and re-upload the files we know work. The CLI is a powerful tool, but makes it easy for things to go wrong.

<h4>2. Always merge your changes into master once work is complete</h4>

After you are done making changes to the SDF project, make sure to create a pull request inside the github repository, and merge your changes into master. This keeps everything up to date, and easy to track.

<h4>3. Tag Using Semantic Versioning</h4>

After merging into the master branch, make sure you tag master properly. <strong>Major/Minor/Update Ex: 1.2.3</strong> This keeps a record of changes that's much easier to track than looking at previously merged branches and commits.




<style>
    .terminal-window {
        background-color:#303030;
        color:#fff;
        padding: 1.5em;
    }
</style>
