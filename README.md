# Find patterns in paths


**path-pattern finder** is a Java library to find naming-patterns in a list of strings or paths, using a particular set of rules. A command-line app for basic usage is also included.



One can translate a set of file-paths into their constant and non-constant (variable) components.



e.g. consider some paths

```
somedir/somefilename_001.txt
somedir/somefilename_002.txt
somedir/somefilename_003.txt
```



In this case, the library would find the pattern:

```
somedir/somefilename_{0}.txt
```

where {0} indexes each component.

## Example

Consider a directory of picture files (with several nested sub-directories).


Files take the form:

```
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Milan\2013-04-02 20.07.42.jpg
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Milan\IMG_4677.JPG
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Milan\IMG_4678.JPG
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Milan\IMG_4682.JPG
...
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Verona\IMG_4252.JPG
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Verona\IMG_4255.JPG
C:\Users\Owen\Pictures\Holidays\Italy at Easter (March 2013)\Verona\IMG_4261.JPG
etc.
```



The command-line app would produce:

```
There are 274 input paths in total

Pattern is: C:\Users\Owen\Pictures\Archived\Holidays\Italy at Easter (March 2013)\${0}\${1}${2}.jpg

${0} = 6 unique strings e.g. "Venice" (145), "Milan" (38), "Verona" (34)
${1} = "IMG_" (273) | "2013-04-02 20.07." (1)
${2} = 274 unique integers between 42 and 4766 inclusive
```
The number in parantheses describes the number of files in a particular category.

# Download

The [latest release](https://github.com/path-pattern-finder/path-pattern-finder-distribution/releases/latest) as well as [source-code](https://github.com/path-pattern-finder/path-pattern-finder) are both available to download on GitHub.

The [latest JARs](https://github.com/path-pattern-finder/path-pattern-finder/packages/126777) are stored in [GitHub Packages](https://github.com/features/packages) maven repository. Note that [authentication is required](https://github.github.com/maven-plugins/site-plugin/authentication.html) via a GitHub token.


# Usage

Either as a Java library, or a command-line tool.

Being pure Java, it works on Windows, Linux, Mac and several other operating systems.

An `.exe` launcher and Linux wrapper-script are included in the [distribution](https://github.com/path-pattern-finder/path-pattern-finder-distribution/releases/latest) for easy command-line use in Windows and Linux.

After unpacking the `zip`/`tar.gz` distribution, it is advisable to add the `bin/` directory to the system path.

## ...as a command-line app


Call ```path-pattern-finder``` as an application with one or more wildcard arguments e.g.

```
path-pattern-finder *.jpg *.png
```

This will

1. recursively search the current working directory for files matching the wildcard arguments (a glob)
2. find the pattern
3. print the pattern to the console
 
## ...as a library

Use the methods in [PathPatternFinder](https://path-pattern-finder.github.io/javadoc/com/owenfeehan/pathpatternfinder/PathPatternFinder.html) to find patterns. e.g. ```findPatternPaths``` or ```findPatternStrings```.

```java
import com.owenfeehan.pathpatternfinder.PathPatternFinder;
Pattern pattern = PathPatternFinder.findPatternPaths(paths, IOCase.INSENSITIVE, true);
```

Or to find the common root-directories of a list of paths, see [FindCommonPathElements](https://path-pattern-finder.github.io/javadoc/com/owenfeehan/pathpatternfinder/commonpath/FindCommonPathElements.html).

```java
import com.owenfeehan.pathpatternfinder.commonpath.FindCommonPathElements;
Optional<Path> commonPath = FindCommonPathElements.findForFilePaths(paths);
```

See the [Javadoc](javadoc/) for more detailed code documentation.


# Applications


* Images from microscopes often come in a sequential manner, with the sequence encoded in the file-path.
* Images from digital-cameras are often sequenced by time or number. 
* The [Anchor image analysis software suite](http://www.anchoranalysis.org) uses the library to guess patterns in image files.

# Source

[Source code](https://github.com/path-pattern-finder/path-pattern-finder) can be found on [GitHub](https://github.com/path-pattern-finder), together with [artifacts](https://github.com/orgs/path-pattern-finder/packages) and [continuous integration](https://github.com/path-pattern-finder/path-pattern-finder/tree/master/.github/workflows). Code quality metrics are found on [SonarCloud](https://sonarcloud.io/dashboard?id=path-pattern-finder_path-pattern-finder).

# Author



[Owen Feehan](http://www.owenfeehan.com) distributed under MIT license.
