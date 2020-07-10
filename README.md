### LeafKit/Leaf4 Xcode Highlighting

Add syntax highlighting for LeafKit templating document files to Xcode 11 & 12:

* Anonymous expressions, tags, and bodied tags will highlight
* All raw, non-Leaf content highlights as "comment" to recede visually
* Parameters will highlight, and bodied tags will fold

This is very preliminary and has several issues:

* Parameters are not actually lexed properly and invalid grammar will highlight (eg, anonymous expressions with parameters rather than a single expression)
* No actual tag matching is done to verify that the end tag name the opening tag for bodied tags.
* Variables and function calls inside a tag are colored the same - EG `#(variable)` & `#(function(variable))`, function and variable should be different colors (but aren't)
* `:` and `#` delineating the start and end of a tag body do not highlight
* Preliminary Leaf4 commenting style is highlighted (see [LeafKit PR #61](https://github.com/vapor/leaf-kit/pull/61)); this also includes parameters spanning multiple lines. These syntax features are **NOT** present in the current (LeafKit-1.0.0-rc.1.16) release.

*this is **NOT** a stable language specification and is subject to breaking in the future.*

<img src="https://raw.githubusercontent.com/tdotclare/media/master/syntaxhighlighting.jpg" style="zoom:50%;" />



This project uses portions of [ApolloGraphQL](https://github.com/apollographql/xcode-graphql) under MIT License as a basis for Xcode plugin & language spec file injection.

### Installation On Xcode 11.5 and Higher

**NOTE**: Tested (as of 7.9.2020) on Xcode 11.5 and Xcode 12beta2 and may break in the future. Please use caution.

### Setup script

If you're running Xcode 11 or higher, the fastest way to install is to `cd` into the directory where this repo has been checked out or downloaded, and run the following command in your terminal:

```
sudo ./setup.sh
```

Once the setup script has finished, restart Xcode and click the "Load bundle" button on the permissions dialog that appears in Xcode when it restarts. 

### Manual installation

**Note**: You probably need to `sudo` to get these commands to work. 

- Copy the `Leaf.ideplugin` directory to `~/Library/Developer/Xcode/Plug-ins/`:

	```
	cp -r Leaf.ideplugin ~/Library/Developer/Xcode/Plug-ins/
	```
- Copy the `Leaf.xclangspec` file to `/Applications/Xcode.app/Contents/SharedFrameworks/SourceModel.framework/Versions/A/Resources/LanguageSpecifications`:

  ```
  cp Leaf.xclangspec /Applications/Xcode.app/Contents/SharedFrameworks/SourceModel.framework/Versions/A/Resources/LanguageSpecifications
  ```

  - Copy the `Xcode.SourceCodeLanguage.Leaf.plist` file to `/Applications/Xcode.app/Contents/SharedFrameworks/SourceModel.framework/Versions/A/Resources/LanguageMetadata`:

  ```
  cp Xcode.SourceCodeLanguage.Leaf.plist /Applications/Xcode.app/Contents/SharedFrameworks/SourceModel.framework/Versions/A/Resources/LanguageMetadata
  ```

### Versions of Xcode prior to 11

This has not been tested on any version of Xcode prior to 11.5. It (probably) should work on any 11.x version, probably would work on older versions, but user beware.
