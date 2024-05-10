# AGON
## Initials Competition Website Package

## Config Options:

### AppSettings Config:
The following options are available for configuration in the appsettings.json file under Agon -> CompetitionSettings:

| Setting Key | Type | Description |
| ------ | ------ | ------ |
| PrizesEnabled | boolean | Are prizes enabled or is the site used for Prize Draw entry only
| FormViewName | string | The path to the view file (cshtml) that will display the competition form on-screen |
| CompetitionModelType | string | The model to load into the competition form view file |
| AllowMultipleEntries | boolean | Should the system allow entries from the same email address |
| MaxEntriesPerDay | int | If 'AllowMultipleEntries' is true then how many times per day can a user enter with the same email address |
| MaxEntriesTotal | int | If 'AllowMultipleEntries' is true then how many can a user enter with the same email address enter in total |
| RedirectOnMaxEntries | string | URL to redirect users to when/if they reach max entry count, leave blank fro no redirect |
| EnableLocalStorageChecks | boolean | If 'AllowMultipleEntries' is true this will also use local storage to minitor entries rather than just email address |
| ArchiveWinningMoments | boolean | If enabled winning moments that pass and are not won/claimed will be marked as archived and will not then be claimable |
| WinningMomentsUploadPath | string | Path on file system where uploads should be temporarily saved during upload of new winning moments file (based on browsable web path) |
| ReportDashboardColumns | string (csv) | Which custom properties should be displayed on the entry report dashboard
| SendWinnerEmail | boolean | When a user wins a prize should they be notified via email

## Starting a new project
When creating a new competition project site follow these steps:

1. Create new visual studio solution/repo
2. Install Umbraco (if not already installed) configure basic Umbraco settings like connection string and create a new empty database if required
3. Add the package 'Initials.Agon.Competitions' or use ```Install-Package Initials.Agon.Competitions```
4. Build solution and ensure you can still access the back office and uSync is now installed (this should be installed as part of step 3)
5. Copy the following files/folder from this repo to your newly created Umbraco project:
    1.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    2.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    3.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    4.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    5.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    6.  [~/wwwroot/backoffice](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/wwwroot/)
    7. [~/App_Plugins](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/App_Plugins/)
    8. [~/uSync](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/uSync/)
    9. [~/Views](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/Views/)
    10. [~/RewriteRules.xml](https://bitbucket.org/ma-initials-co-uk/initials.agon/src/main/Initials.Agon.Web/)
6. Ensure you have added the config/settings options into the appsettings.json file (see above)
7. Edit ***Startup.cs*** to include the following:
```
// add under ConfigureServices to ensure default page handler is added

// use agon default renderer to check for start dates
services.UseDefaultRenderController();

```
```
// add error page handler
if (env.IsDevelopment())
{
	app.UseDeveloperExceptionPage();
}
else
{
	app.UseExceptionHandler("/500.html");
}

```
```
// add rewrite rule handler
app.UseRewriteRulesXmlFile();
```
```
app.UseRewriteRulesXmlFile();

// add sitemap and robots handlers
u.EndpointRouteBuilder.MapControllerRoute("Robots.txt Handler",
    "/robotstxt",
    new { Controller = "RobotsTxt", Action = "Index" });
u.EndpointRouteBuilder.MapControllerRoute("Sitemap Controller",
    "/sitemapxml",
    new { Controller = "Sitemap", Action = "Index" });
```




## Package Deployment Help

To publish this package to a private NuGet feed you need to do the following.

### First time setup

If this is the first time you have executed this process you will need to complete the following steps first:

1. Download NuGet.exe from [https://go.microsoft.com/fwlink/?linkid=2099732](https://go.microsoft.com/fwlink/?linkid=2099732) install this into a folder on your c:\ drive and add the path to your PATH variable for the system
2. Download the credential provider from [https://github.com/microsoft/artifacts-credprovider#setup](https://github.com/microsoft/artifacts-credprovider#setup) see the guide under **Automatic PowerShell script**
3. Download and install the dotnet core SDK  from [https://go.microsoft.com/fwlink/?linkid=2103972](https://go.microsoft.com/fwlink/?linkid=2103972)
4. Add the custom feed to your visual studio settings

### Building the package

1. Increase the assembly version number
2. Run the batch file '**Publish.Agon.Package.bat**'

### Custom User Groups

| User Groups Name | User Group ID | Description | Permissions |
| ---------------- | ------------- | ----------- | ----------- |
| Dashboard Access - Data Entry Reports | dataEntryReports | Allows the user to view the Data Entry report dashboard and view/export all entry records | Content, Media |
| Dashboard Access - Winning Moment | winningMomentsEditor | Allows the user to view the Winning moments in the system and import new/update records | Content, Media |