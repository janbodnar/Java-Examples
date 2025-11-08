# Java-Examples

To goal of this repository is to provide Java code examples to learn the Java basics  
quickly. It uses modern Java features. 

Repeat with formatted:

```java
void main() {

  IO.println("hello %s%n".repeat(3).formatted("Jan", "Eva", "Mia"));
}
```


Set the libraries for VS Code to recognize them in simple Java examples. 

```json
{
    "java.project.referencedLibraries": [
        "jsoup-1.21.2.jar",
        "sdk-1.10.0.jar",
        "gson-2.10.1.jar"
    ]
}
```

## VS Code settings

VS Code settings related to Java:

```json
{
  "editor.minimap.enabled": false,
  "editor.fontFamily": "Cascadia Code",
  "chat.fontSize": 16,
  "chat.editor.fontSize": 15,
  "editor.fontSize": 16,
  "editor.stickyScroll.enabled": false,
  "terminal.integrated.stickyScroll.enabled": false,
  "java.configuration.runtimes": [
    {
      "name": "JavaSE-25",
      "path": "/home/jano/.sdkman/candidates/java/25-amzn/",
      "default": true
    }
  ],
  "java.inlayHints.parameterTypes.enabled": false,
  "java.format.settings.url": "file:///home/jano/Documents/eclipse-java-formatter.xml",
  "java.format.settings.profile": "2-space-indent",
  "[java]": {
    "editor.tabSize": 2,
    "editor.detectIndentation": false,
    "editor.insertSpaces": true,
    "editor.indentSize": 2,
    "editor.wrappingIndent": "none",
  },
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": false,
    "scminput": false,
    "java": true
  },
  "editor.tabSize": 2,
  "editor.detectIndentation": false,
  "editor.insertSpaces": true,
  "editor.indentSize": 2,
  "editor.wrappingIndent": "none",
  "editor.formatOnPaste": true,
  "sonarlint.focusOnNewCode": false
}
```

## Eclipse Java formatter

The formatter is set in the `settings.json`:

`"java.format.settings.url": "file:///home/jano/Documents/eclipse-java-formatter.xml",`

The file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<profiles version="12">
    <profile kind="CodeFormatterProfile" name="2-space-indent" version="12">
        <setting id="org.eclipse.jdt.core.formatter.tabulation.char" value="space"/>
        <setting id="org.eclipse.jdt.core.formatter.tabulation.size" value="2"/>
        <setting id="org.eclipse.jdt.core.formatter.indentation.size" value="2"/>
        <setting id="org.eclipse.jdt.core.formatter.continuation_indentation" value="2"/>
        <setting id="org.eclipse.jdt.core.formatter.lineSplit" value="80"/>
        <setting id="org.eclipse.jdt.core.formatter.alignment_for_arguments_in_method_invocation" value="16"/>
    </profile>
</profiles>
```
