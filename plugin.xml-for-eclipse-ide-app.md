We already know how to [program "plugin.xml" for RCP app](plugin.xml-for-eclipse-rcp-app). 

Programming "plugin.xml" for IDE app is not much different. There is only one difference: Wuff does not generate extension-point "org.eclipse.core.runtime.applications" for IDE apps. Instead, it uses the extension-point "org.eclipse.ui.ide.workbench", provided by Eclipse libraries.

---

Next page: ["plugin.xml" expression injection](plugin.xml-expression-injection)