# Wings-Sass
CSS generator for ASNA Monarch and ASNA Wings Websites

ASNA Monarch/Wings websites contain two basic Cascading Style Sheets (CSS), namely:

1. Framework.css
2. Theme.css

These CSS files are created in the folder: ~Themes\Current\Styles folder, *where ~ represents the root website folder.*

#### Framework.css 
Defines the CSS classes that the ASNA Web Controls will use. The names of all ASNA Web controls share the prefix “Dds,” like DdsCharField, DdsConstant, etc.

Given that Monarch/Wings website pages (displayfiles) are produced by importing display specifications from DDS source members, Framework.css contains styles that have been carefully selected to produce Web Pages with high fidelity to the legacy positions and field lengths designed for the IBM i. In particular, for constants and fields to align, the Framework font styles are set to a monospaced family, and all fields’ styles are set to work on a grid-like display.

As a rule, do not change the contents of this file.

#### Theme.css
Defines the CSS classes that establish the overall website style. 
Other styles in Theme.css,

1. Define a particular company's branding. There are components of Monarch/Wings Web page that may be rendered using a more modern style, such as function key menus, Pop-up Windows, and other container labels.
2. Override the CSS classes defined in Framework.css. 

### Minifying CSS Resources

"Minifying"  a resource is a very simple way to improve performance (reducing the time a website response page takes to be transmitted from the server to the client device).

The process of minification consists of reducing the size of a resource (in this case the CSS file) without losing any of the required syntax imposed by the CSS standard. The Wings-Sass project, in addition to producing the Framework.css and Theme.css, also produce the minified CSS files: Framework.min.css and Theme.min.css.

To use the minified CSS, all you need to do is copy these files to your ~Themes\Current\Styles folder and update the references on your MasterPage(s) to point to the `.min.css` instead of the `.css`

### Optimization beyond Minification

When your Monarch/Wings site is complete, you may want to review the list of ASNA Web Controls used for controls that are NOT being used, to remove the related CSS styles. For example, if your Monarch/Wings website does not use the 5250 Terminal Emulator, you can easily remove a big chunk from `Framework.css` making the size of the minified version even smaller. (Read the section `Removing Unused CSS Styles to Optimize Response Time` below).


## Installation

1. Locate the "Download ZIP" button on this page.
2. Click on the "Download ZIP" button.
3. Save the file in a temporary folder on your PC.
4. Extract the files in the downloaded zip file.
5. Copy all the files into your Monarch/Wings ~Themes\Current\Styles folder.
6. Notice that all the files in this repository have the extension `.scss`. This extension identifies the file as Sass (Syntactically Awesome Cascasing Style Sheet). Note also that except for `Framework.scss` and `Theme.scss` the files in this project start with `_` (underscore). Files that start with underscore do not produce directly a CSS file with the same name (these files are *include* files part of the main Sass files that refer to them).  

  * Visual Studio 2013: To facilitate working with Sass, install the Microsoft *"Web Essentials"* package for Visual Studio 2013 from here: 
   https://visualstudiogallery.msdn.microsoft.com/56633663-6799-41d7-9df7-0f2a504ca361 The *"Web Essentials"* package was designed such that right after saving changes to any of the Sass files, the compiler will wake-up and produce a new CSS automatically.
   
  * Visual Studio 2015: To facilitate working with Sass, go to "Tools" menu and select "Extensions and Updates" option. On the dialog box that appears, click on the "online" extensions, and look for "Web Compiler". Once the "Web compiler" extension is installed, you can right-click on any of the Sass files in your website, and an explicit "Re-compile file" menu option will be available. Re-compiling a Sass file produces the CSS and min.CSS files.
   
  Sass is designed to compile the Sass files (producing CSS) as soon as changes on files are saved. For more information on Sass, please refer to http://sass-lang.com

## Usage

If the installation is complete, your folder ~Themes\Current\Styles will have new `Framework.css, Framework.min.css, Theme.css` and `Theme.min.css` files.

Locate the file '_config.scss` in the ~Themes\Current\Styles folder.

This file lists a series of constants used by the CSS class definitions in all the Wings-Sass project. Each of the constants starts with the symbol `$`, and define a CSS attribute. For example:

`$dds-field-error-background-color: #c00;`

One of the CSS classes that uses that constant is:


```
.DdsCharField_Error {
    @extend .DdsCharField;
    color: $dds-field-error-color;
    background-color: $dds-field-error-background-color;
}
```

Other CSS classes defined in this project share that constant. 

To customize your Framework.css and Theme.css, change the value associated with the constants; as soon as you save the _config.scss, you can verify that the resulting `Framework.css, Framework.min.css, Theme.css` and `Theme.min.css` files are automatically updated.

### Update your MasterPage(s)

When you use this Wings-Sass project, you may want to update your MasterPage(s) to reference the minified versions of the CSS.

1. Locate the file: `~\Themes\Current\MasterPage.master`
2. Locate the following lines in the markup:

    ```
    <link rel="stylesheet" type="text/css" href="~/Themes/Current/Styles/Framework.css">
    <link rel="stylesheet" type="text/css" href="~/Themes/Current/Styles/Theme.css">
    ```

3. Update the filenames by adding `.min.` to the extension:

    ```
    <link rel="stylesheet" type="text/css" href="~/Themes/Current/Styles/Framework.min.css">
    <link rel="stylesheet" type="text/css" href="~/Themes/Current/Styles/Theme.min.css">
    ```
4. Finally, review any other Master pages (such as MasterPage.Window.master), and repeat steps 2 and 3 (above).    

### Removing Unused CSS Styles to Optimize Response Time.

Let's assume that after completing your Monarch/Wings website, right before testing, you have determined that 5250 Terminal support is not needed.

To remove unused CSS syles, do the following:

1. Edit `Framework.scss`
2. Locate the following @import block:

    ```
    @import "_ddsconstant";
    @import "_ddscharfield";
    @import "_ddsdecfield";
    @import "_ddsdecdatefield";
    @import "_ddstimefield";
    @import "_ddstimestampfield";
    @import "_ddsrecord";
    @import "_ddswindowrecord";
    @import "_ddssubfile";
    @import "_calendar";
    @import "_5250";
    @import "_ddspanel";
    @import "_ddschart";
    @import "_ddsimage";
    @import "_ddssignature";
    @import "_ddsswitch";
    ```

3. Assuming you want to eliminate CSS styles related to 5250 Terminal Emulation, the line we want to remove is `@import "_5250"`. You can delete that line, or better yet, comment it out by adding two back-slashes in front of it:

    ```
    \\ @import "_5250";
    ```
4. Save your changes. The new `Framework.css` and `Framework.min.css` will be automatically updated.

## License



## Contributions
