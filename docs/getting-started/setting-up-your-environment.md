# Setting Up Your Development Environment

Setting up your development environment is an important first step to beginning development work.

<hr />

## Software Requirements

<h4 id="vs-code">VS Code</h4>
First thing we need to do is download and install Microsoft VS Code. VS Code is one of NetSuite's preferred IDE's, which makes it ideal for what we're doing here.<br />

[Download VS Code](https://code.visualstudio.com/)

<hr />

<h4 id="homebrew">Homebrew</h4>
Assuming you're developing on Mac, you will want to download and install homebrew on your computer. Homebrew is a fairly standard package manager used for OSX and will help you install other software packages such as the Java Development Kit we will need.<br />

[Install Homebrew](https://brew.sh/)

You can check to see if your homebrew installation was completed successfully by running: <xmp>homebrew -v</xmp> If a version number is returned, then you know it works!

<hr />

<h4 id="node-js">Node.js</h4>
Node.js is a requirement for developing basically any JavaScript application. When you install Node.js, you will be able to use npm, or Node Package Manager. This is how we install JavaScript packages in projects and generate JavaScript projects themselves. You can read more about Node.js <a href="https://nodejs.org/en" target="_blank">here</a>.

[Install Node.js](https://nodejs.org/en)

You can check to see if your Node.js installation was successful by running: <xmp>node -v</xmp> and <xmp>npm -v</xmp> They should both return their respective version numbers.

> NOTE: Double check inside of NetSuite's or other software's documentation to make sure the currently installed version of Node.js is correct, and fully compatible

<hr />

## Java Development Kit
<span id="jdk" />
One of the requirements to run NetSuite's CLI (Command Line Interface) is JDK 17, or JDK 21. (we're currently using JDK 21 as of right now).<br />
Using Homebrew, install JDK 21:

<xmp>
brew install openjdk@21
sudo ln -sfn /opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-21.jdk
</xmp>

> NOTE: If JDK 17 is needed, the version number can be substituded inside the above statements.

Then we add it to our .zshrc or .bash_profile:

<xmp>
export JAVA_HOME="$(/usr/libexec/java_home -v21)"
export PATH="$JAVA_HOME/bin:$PATH"
</xmp>

<hr />

## NetSuite CLI & API
<span id="netsuite-cli" />
NetSuite was kind enough to provide us with a handy CLI that makes interacting with the file cabinet and SuiteScripts a much more streamlined experience, especially for development.

Install SuiteCloud CLI:

<xmp>
npm install -g @oracle/suitecloud-cli
</xmp>

Verify the install

<xmp>
suitecloud --version
</xmp>

<hr />

<strong>Congratulations!</strong> You now have a fully ready to work software development environment tailored for NetSuite and Suntado!

