# BUILD

To create a build, which can be deployed to a web server, the following needs to be considered:

- In Visual Studio, with the solution opened, change the **Build Project Order** so that all projects in the
  Plugins folder, are depending on Nop.Web. This makes sure, that the Plugins outputs are copied to the build
  output folder.

- The following two projects have dependencies to **Nop.Web** and can therefore not by selected for dependency.
  As soon as we need them, we will have to find a solution.

    - Nop.Plugin.Payments.Square
    - Nop.Plugin.Payments.Worldpay

- Use ````msbuild NopCommerce.sln /p:DeployOnBuild=true /p:WebPublishMethod=Package /p:PackageAsSingleFile=true /p:SkipInvalidConfigurations=true /p:PackageLocation="C:\DATA\BUILD\nopcommerce" /p:platform="any cpu" /p:configuration="release"````
  to build packages.

- One package is created, **Nop.Web.zip**. This can be used to deploy to a IIS web server

# DEVELOPMENT ENVIRONMENT

## DIFFERENT RELEASE BRANCHES | SETUP A NEW DATABASE

If you change branches (with different releases) make sure that you setup a new database
by deleting the folloing folders, before building the solution:

- Nop.Web\App_Data\dataSettings.json
- Nop.Web\App_Data\plugins.json
- Plugins\**

When you start the application, you should now be asked for creating a new database.
