# BUILD

To create a build, which can be deployed to a web server, the following needs to be considered:

- In Visual Studio, with the solution opened, change the **Build Project Order** so that all projects in the
  Plugins folder, are depending on Nop.Web. This makes sure, that the Plugins outputs are copied to the build
  output folder.

- In **Nop.Web.csproj** change the following from
  ````<Folder Include="Plugins\bin\" />````
  to
  ````<Folder Include="Plugins\" />````.
  This makes sure, that the plugins, which are compiled into the **Plugins** folder, are copied by MSBUILD
  to the output folder.

- Use ````msbuild NopCommerce.sln /p:DeployOnBuild=true /p:WebPublishMethod=Package /p:PackageAsSingleFile=true /p:SkipInvalidConfigurations=true /p:PackageLocation="C:\DATA\BUILD\nopcommerce" /p:platform="any cpu" /p:configuration="release"````
  to build packages.

- Two packages are created, **Nop.ADMIN.zip** and **Nop.Web.zip**. They can be used to deploy to a IIS web server

- When using MS DEPLOY to deploy to the web server, make sure **Nop.ADMIN.zip** is deployed before **Nop.Web.zip**
  because otherwise **web.config** of ADMIN would override the **web.config** of WEB

# DEVELOPMENT ENVIRONMENT

## DIFFERENT RELEASE BRANCHES | SETUP A NEW DATABASE

If you change branches (with different releases) make sure that you setup a new database
by deleting the folloing folders, before building the solution:

- Nop.Web\App_Data\dataSettings.json
- Nop.Web\App_Data\plugins.json
- Plugins\**

When you start the application, you should now be asked for creating a new database.
