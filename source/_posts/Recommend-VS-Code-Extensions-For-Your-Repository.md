---
title: Project Recommended VS Code Extensions
date: 2017-02-04 14:53:00
tags: VS Code, Boost
---
One of my favorite aspects of [Visual Studio Code](https://code.visualstudio.com/) is the vibrant library of commumnity created extensions. While the IDE is great out of the box, these extensions give an added boost you just can't live without.

When developing an application with a framework like Angular, there may be a handful of extensions your team finds useful to use. VS Code makes sharing these extentions is actually quite easy.

Open the command pallet (`F1`) and type `Extensions: Configured Recommended Extensions (Workspace)`. This will create a file named `extensions.json` in your `.vscode` folder. Edit the file by supplying a list of extensions by `${publisher}.${name}`. For example:

```javascript extensions.json
{
	// See http://go.microsoft.com/fwlink/?LinkId=827846
	// for the documentation about the extensions.json format
	"recommendations": [
		// Extension identifier format: ${publisher}.${name}. Example: vscode.csharp
		msjsdiag.debugger-for-chrome  // Debugging In Chrome
	]
}
```
The publisher of the extension is listed beside the extension name when you open the extension in the Marketplace. Add a comment next to each extension to specify why the extension is useful. Save and commit to the repository.

{% img /assets/images/vs-code.jpg %}

Next time a team member opens the project in VS Code, they will be greeted with a message to install the workspace's recommended extensions. 



 