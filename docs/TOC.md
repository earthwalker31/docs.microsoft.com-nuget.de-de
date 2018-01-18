# [Was ist NuGet?](What-is-NuGet.md)
# Schnellstart
## [Erstellen und Veröffentlichen eines Pakets](Quickstart/Create-and-Publish-a-Package.md)
## [Verwenden eines Pakets](Quickstart/Use-a-Package.md)
# Führungslinien
## [Installieren von NuGet-Clienttools](Guides/Install-NuGet.md)
## [Erstellen von .NET Standard-Paketen (Visual Studio 2017)](Guides/Create-NET-Standard-Packages-VS2017.md)
## [Erstellen von .NET Standard-Paketen (Visual Studio 2015)](Guides/Create-NET-Standard-Packages-VS2015.md)
## [Erstellen von UWP-Paketen](Guides/Create-UWP-Packages.md)
## [Erstellen von UWP-Steuerelementen als NuGet-Pakete](Guides/Create-UWP-Controls.md)
## [Erstellen plattformübergreifender Pakete](Guides/Create-Cross-Platform-Packages.md)
## [Abfrage für alle Pakete mithilfe der API](Guides/api/query-for-all-published-packages.md)
# Erstellen von Paketen
## [Übersicht und Workflow](Create-Packages/Overview-and-Workflow.md)
## [Erstellen eines Pakets](Create-Packages/Creating-a-Package.md)
## [Unterstützen mehrerer Zielframeworks](Create-Packages/Supporting-Multiple-Target-Frameworks.md)
## [Umwandlungen von Quellcode und Konfigurationsdateien](Create-Packages/Source-and-Config-File-Transformations.md)
## [Erstellen von lokalisierten Paketen](Create-Packages/Creating-Localized-Packages.md)
## [Vorabversionspakete](Create-Packages/Prerelease-Packages.md)
## [Native Pakete](Create-Packages/Native-Packages.md)
## [Symbolpakete](Create-Packages/Symbol-Packages.md)
## [Veröffentlichen eines Pakets](Create-Packages/Publish-a-package.md)
## [„project.json“ und UWP](Create-Packages/project-json-and-UWP.md)
## [Auswirkungen von „project.json“](Create-Packages/project-json-Impact.md)
# Nutzen von Paketen
## [Übersicht und Workflow](Consume-Packages/Overview-and-Workflow.md)
## [Suchen und Auswählen von Paketen](Consume-Packages/Finding-and-Choosing-Packages.md)
## [Paketwiederherstellung](Consume-Packages/Package-Restore.md)
### [Problembehandlung](Consume-Packages/Package-restore-troubleshooting.md)
## [Installieren und Aktualisieren von Paketen](Consume-Packages/Reinstalling-and-Updating-Packages.md)
## [Pakete und Quellcodeverwaltung](Consume-Packages/Packages-and-Source-Control.md)
## [Verwalten des NuGet-Caches](Consume-Packages/Managing-the-NuGet-Cache.md)
## [Konfigurieren von NuGet-Verhalten](Consume-Packages/Configuring-NuGet-Behavior.md)
## [Abhängigkeitsauflösung](Consume-Packages/Dependency-Resolution.md)
## [Paketverweise in Projektdateien](Consume-Packages/Package-References-in-Project-Files.md)
# Hosten von Paketen
## [Übersicht](Hosting-Packages/Overview.md)
## [Lokale Feeds](Hosting-Packages/Local-Feeds.md)
## [NuGet.Server](Hosting-Packages/NuGet-Server.md)
# Tools
## [Referenz zur nuget.exe-CLI](tools/nuget-exe-CLI-Reference.md)
### [add](Tools/cli-ref-add.md)
### [config](Tools/cli-ref-config.md) 
### [delete](Tools/cli-ref-delete.md) 
### [help oder ?](Tools/cli-ref-help.md)
### [init](Tools/cli-ref-init.md) 
### [install](Tools/cli-ref-install.md)
### [list](Tools/cli-ref-list.md) 
### [locals](Tools/cli-ref-locals.md)
### [mirror](Tools/cli-ref-mirror.md)
### [pack](Tools/cli-ref-pack.md) 
### [push](Tools/cli-ref-push.md) 
### [restore](Tools/cli-ref-restore.md)
### [setapikey](Tools/cli-ref-setapikey.md)
### [sources](Tools/cli-ref-sources.md) 
### [spec](Tools/cli-ref-spec.md) 
### [update](Tools/cli-ref-update.md)
### [Umgebungsvariablen](Tools/cli-ref-environment-variables.md)
## [Benutzeroberfläche des Paket-Managers](Tools/Package-Manager-UI.md)
## [Paket-Manager-Konsole](Tools/Package-Manager-Console.md)
## [PowerShell-Referenz](Tools/PowerShell-Reference.md)
### [Add-BindingRedirect](Tools/ps-ref-add-bindingredirect.md)
### [Find-Package](Tools/ps-ref-find-package.md)
### [Get-Package](Tools/ps-ref-get-package.md)
### [Get-Project](Tools/ps-ref-get-project.md)
### [Install-Package](Tools/ps-ref-install-package.md)
### [Open-PackagePage](Tools/ps-ref-open-packagepage.md)
### [Sync-Package](Tools/ps-ref-sync-package.md)
### [Uninstall-Package](Tools/ps-ref-uninstall-package.md)
### [Update-Package](Tools/ps-ref-update-package.md)
## [dotnet-Befehle](Tools/dotnet-Commands.md)
# Verweis
## [.nuspec](Schema/nuspec.md)
## [packages.config](Schema/packages-config.md)
## [project.json](Schema/project-json.md)
## [Paketversionsverwaltung](reference/package-versioning.md)
## [Datei „Nuget.Config“](Schema/nuget-config-file.md)
## [MSBuild-Ziele](Schema/msbuild-targets.md)
## [Zielframeworks](Schema/Target-Frameworks.md)
## [Konventionen für Analysetools](Schema/Analyzers-Conventions.md)
## [Fehler und Warnungen](Reference/Errors-and-Warnings.md)
## [ID-Präfix-Reservierung](Reference/ID-Prefix-Reservation.md)
## [NuGet-Client SDK](Reference/nuget-client-sdk.md)
## Erweiterungen
### [NuGet-Anmeldeinformationsanbieter für Visual Studio 2017](Reference/extensibility/Nuget-Credential-Providers-for-Visual-Studio.md)
### [„nuget.exe“-Anmeldeinformationsanbieter](Reference/extensibility/nuget-exe-Credential-Providers.md)
# API
## [Übersicht](API/overview.md)
## [Dienstindex](API/service-index.md)
## [Per Push Übertragen und Löschen](API/package-publish-resource.md)
## [Suchen](API/search-query-service-resource.md)
## [AutoVervollständigen](API/search-autocomplete-service-resource.md)
## [Metadaten von Paketen](API/registration-base-url-resource.md)
## [Paketinhalt](API/package-base-address-resource.md)
## [URL für das Melden von Missbrauch](API/report-abuse-resource.md)
## [Katalog](API/catalog-resource.md)
## [„nuget.org“-Protokolle](API/nuget-protocols.md)
# Visual Studio-Erweiterbarkeit
## [NuGet-API in Visual Studio](Visual-Studio-Extensibility/NuGet-API-in-Visual-Studio.md)
## [Projektsystemunterstützung](Visual-Studio-Extensibility/Project-System-Support.md)
## [Visual Studio-Vorlagen](Visual-Studio-Extensibility/Visual-Studio-Templates.md)
# Richtlinien
## [NuGet: häufig gestellte Fragen](Policies/NuGet-FAQ.md)
## [Governance](Policies/Governance.md)
## [Ökosystem](Policies/Ecosystem.md)
## [Konfliktlösung](Policies/Dispute-Resolution.md)
## [Löschen von Paketen](Policies/Deleting-Packages.md)
# [GitHub-Repositorys](https://github.com/NuGet)
# Anmerkungen zu dieser Version
## [Bekannte Probleme](Release-Notes/Known-Issues.md)
## [NuGet 4.5 RTM](Release-Notes/NuGet-4.5-RTM.md)
## [NuGet 4.4 RTM](Release-Notes/NuGet-4.4-RTM.md)
## [NuGet 4.3 RTM](Release-Notes/NuGet-4.3-RTM.md)
## [NuGet 4.0 RTM](Release-Notes/NuGet-4.0-RTM.md)
## [NuGet 4.0 RC](Release-Notes/NuGet-4.0-RC.md)
## [NuGet 3.5 RTM](Release-Notes/NuGet-3.5-RTM.md)
## [NuGet 3.5 RC](Release-Notes/NuGet-3.5-RC.md)
## [NuGet 3.5 Beta2](Release-Notes/NuGet-3.5-Beta2.md)
## [NuGet 3.5 Beta](Release-Notes/NuGet-3.5-Beta.md)
## [NuGet 3.4.4](Release-Notes/NuGet-3.4.4.md)
## [NuGet 3.4.3](Release-Notes/NuGet-3.4.3.md)
## [NuGet 3.4.2](Release-Notes/NuGet-3.4.2.md)
## [NuGet 3.4.1](Release-Notes/NuGet-3.4.1.md)
## [NuGet 3.4](Release-Notes/NuGet-3.4.md)
## [NuGet 3.4 RC](Release-Notes/NuGet-3.4-RC.md)
## [NuGet 3.3](Release-Notes/NuGet-3.3.md)
## [NuGet 3.2.1](Release-Notes/NuGet-3.2.1.md)
## [NuGet 3.2](Release-Notes/NuGet-3.2.md)
## [NuGet 3.2 RC](Release-Notes/NuGet-3.2-RC.md)
## [NuGet 3.1.1](Release-Notes/NuGet-3.1.1.md)
## [NuGet 3.1](Release-Notes/NuGet-3.1.md)
## [NuGet 3.0.0](Release-Notes/NuGet-3.0.0.md)
## [NuGet 3.0 RC2](Release-Notes/NuGet-3.0-RC2.md)
## [NuGet 3.0 RC](Release-Notes/NuGet-3.0-RC.md)
## [NuGet 3.0 Beta](Release-Notes/NuGet-3.0-Beta.md)
## [NuGet 3.0 Preview](Release-Notes/NuGet-3.0-Preview.md)
## [NuGet 2.12](Release-Notes/NuGet-2.12.md)
## [NuGet 2.12 RC](Release-Notes/NuGet-2.12-RC.md)
## [NuGet 2.9 RC](Release-Notes/NuGet-2.9-RC.md)
## [NuGet 2.8.7](Release-Notes/NuGet-2.8.7.md)
## [NuGet 2.8.6](Release-Notes/NuGet-2.8.6.md)
## [NuGet 2.8.5](Release-Notes/NuGet-2.8.5.md)
## [NuGet 2.8.3](Release-Notes/NuGet-2.8.3.md)
## [NuGet 2.8.2](Release-Notes/NuGet-2.8.2.md)
## [NuGet 2.8.1](Release-Notes/NuGet-2.8.1.md)
## [NuGet 2.8](Release-Notes/NuGet-2.8.md)
## [NuGet 2.7.2](Release-Notes/NuGet-2.7.2.md)
## [NuGet 2.7.1](Release-Notes/NuGet-2.7.1.md)
## [NuGet 2.7](Release-Notes/NuGet-2.7.md)
## [NuGet 2.6.1-for-WebMatrix](Release-Notes/NuGet-2.6.1-for-WebMatrix.md)
## [NuGet 2.6](Release-Notes/NuGet-2.6.md)
## [NuGet 2.5](Release-Notes/NuGet-2.5.md)
## [NuGet 2.2.1](Release-Notes/NuGet-2.2.1.md)
## [NuGet 2.2](Release-Notes/NuGet-2.2.md)
## [NuGet 2.1](Release-Notes/NuGet-2.1.md)
## [NuGet 2.0](Release-Notes/NuGet-2.0.md)
## [NuGet 1.8](Release-Notes/NuGet-1.8.md)
## [NuGet 1.7](Release-Notes/NuGet-1.7.md)
## [NuGet 1.6](Release-Notes/NuGet-1.6.md)
## [NuGet 1.5](Release-Notes/NuGet-1.5.md)
## [NuGet 1.4](Release-Notes/NuGet-1.4.md)
## [NuGet 1.3](Release-Notes/NuGet-1.3.md)
## [NuGet 1.2](Release-Notes/NuGet-1.2.md)
## [NuGet 1.1](Release-Notes/NuGet-1.1.md)