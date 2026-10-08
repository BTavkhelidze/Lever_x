1. Know the standard folder structure of the SAPUI5
app.

A Standard SAPUI5 application usually has the webapp folder as its main source directory.
inside webapp, we normally orginaze the application according to it's responsibilies. The view folder contains UI definitions, usually XML Views, while controller folder contains controllers responsible for handling UI evnts and application behavior.
The model folder can contain model-related utilities or model creation logic, i18n contains resource bundles for internationalization and fragments can be used for reusability ui parts such as dialogs.
Two important files ara Component.js and manifest.json. component.js represents the application component and contains initialization logic, while manifest.json is the application descriptor where we declaratively configure things like dependencies, models, data sources, routing and other apllication settings.
we can also have a index.html, espicially for standalone execution. it serves as the HTML entry point where SAPUI can be boostrapped and the application component can be started. When the application runs inside the Fiori Launchpad, however, the launchpad provides the bootstrap environment, so the applications index.html is not used as the main entry point. we can also have a test folder for QUnit and OPA5 tests. 
At the project level, outside webapp, we normally have files such as ui5.yaml for UI5 Tooling configuration and package.json for npm dependencies and scripts. 

2. Know the aspects of Component & Manifest:
a. Component definition.
b. Manifest structure.


In a typical SAPUI5 application, Component.js represents the application component. For UI applications it normally extends "sap.ui.core.UIComponent". It is responsible for application-level initialization, and we can override lifecycle methods such as "init" to perform custom initialization. When overriding "init", we first call the parent UIComponent implementation and then execute our own initialization logic.
The component is usually connected to manifest.json through "metadata: { manifest: "json" }". The manifest contains the declarative configuration of the application, while Component.js is used when programmatic initialization or custom logic is required
The manifest is mainly divided into sections such as sap.app, sap.ui, and sap.ui5. sap.app contains general application metadata and data sources, sap.ui contains general UI-related information, and sap.ui5 contains UI5-specific configuration such as dependencies, models, resources and routing.
For example, an OData service can be defined as a data source under sap.app, and a model under sap.ui5 can reference that data source.

3. Be aware of UI5 framework versioning system:
major/minor/patch versions

UI5 versions are represented using major, minor and patch numbers. For example, in version 1.120.7, 1 is the major version, 120 is the minor version and 7 is the patch version.
A major version represents a major framework version line and can involve significant compatibility changes. Minor versions typically introduce new features, APIs and enhancements, while patch versions mainly provide bug fixes and corrections within the same minor release.
As a UI5 developer, the framework version is important because APIs and features may only be available starting from a specific UI5 version. We can also specify minUI5Version in the sap.ui5.dependencies section of the manifest to describe the minimum UI5 version required by the application.


4. Know the different ways of app bootstrapping:
a. Standalone app.
b. flpSandbox app.
c. flpMockServer app.
d. unit/OPA test run app.
e. CDN/local sdk references.

SAPUI5 and starts the application component.
For local testing in a Fiori Launchpad-like environment, we can use an FLP sandbox. In this case, the sandbox initializes the Launchpad environment and then loads our application component.
We can also use an FLP mock server scenario, which additionally starts a mock server so that the application can work with simulated OData/backend data without requiring the real backend.
For automated testing, we can have dedicated QUnit or OPA5 test runner pages. They bootstrap UI5 with the required testing libraries and execute unit or integration tests.
Finally, the UI5 framework itself can be referenced from different locations. For example, we can use locally resolved SDK resources or load UI5 from a CDN

“What is the difference between index.html and flpSandbox.html?”
index.html runs the application standalone, while flpSandbox.html first creates a Fiori Launchpad-like environment and loads the application inside that environment

“What is the difference between flpSandbox and flpMockServer?”
Both can provide an FLP-like environment, but the mock server scenario additionally simulates the backend service and data.

“Why would you use a mock server?”
To develop and test the frontend independently of the real backend, for example when the backend is unavailable or not yet implemented.


5. Know the configuration options and URL parameters of
the app.

In SAPUI5, we can configure the application and the UI5 runtime using bootstrap configuration options and URL parameters.
For example, during bootstrap we can configure the UI5 theme, asynchronous loading, compatibility version, resource roots, and initialization module. Typical options are sap-ui-theme, sap-ui-async, sap-ui-compatVersion, and sap-ui-resourceRoots.
We can also use URL parameters to influence the runtime, especially during development and testing. For example, sap-ui-debug=true enables debug mode, sap-language can be used to specify the language, and sap-ui-theme can be used to override the theme.
I also distinguish URL query parameters from the URL hash. Query parameters can influence configuration, while the hash is normally used by the UI5 router for application navigation.