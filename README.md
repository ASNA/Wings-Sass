# Wings-Sass
CSS generator for ASNA Monarch and ASNA Wings Websites

ASNA Monarch/Wings websites contain two basic Cascading Style Sheets (CSS), namely:

1. Framework.css
2. Theme.css

These CSS files are created in the folder: ~Themes\Current\Styles folder, *where ~ represents the root website folder.*

#### Framework.css 
Defines the CSS classes that the ASNA Web Controls will use. All the ASNA Web controls are named with the prefix Dds, like DdsChanField, DddsConstant, etc.

Given that Monarch/Wings websites pages (displayfiles) are produced by importing display specifications by reading DDS source members, the Framework.css has been carefully selected with styles that produce Web Pages with high fidelity to the legacy positions and length of fields designed for the IBMi. In particular, for constants and fields to align, the Framework font style is set a monospaced family, and all field's styles are set to work on a grid-like display.

As a rule, do not change the contents of this file.

#### Theme.css
Defines the CSS classes that establish the overall website style. 
Other styles in Theme.css,

1. Define a particular company's branding. There are components of Monarch/Wings Web page, that may be rendered using a more modern style, such as function key menus, Popu-up Window, and other container chrome labels.
2. Override the CSS classes defined in Framework.css. 

### Minifying CSS Resources

A very simple way to improve the performance (reducing the time a website response page to be transmitted from the server to the client device), is a technique called "Minifying" a resource. 

The process of minification constist of reducing the size of a resource (in this case the CSS file) without losing any of the required syntax imposed by the CSS standard.
The Wings-Sass project, in addition to producing the Framework.css and Theme.css, also produce the minified CSS files: Framework.min.css and Theme.min.css.

To use the minified CSS, all you need to do is copy these files to your ~Themes\Current\Styles folder and update the references on your MasterPage(s) to point to the`.min.css` instead of the `.css`

### Optimization beyond Minification

When your Monarch/Wings is complete, you may want to review the list of ASNA Web cotrols used, looking for controls that are NOT being used, to remove the related CSS styles. For example, if your Monarch/Wings website does not use the 5250 Terminal Emulator, you can easily remove a big chunk from `Framework.css` making the size of the minified version even smaller. (Read the section `Removing unused CSS styles to Optimize response time` below)


## Installation

1. Locate the the "Download ZIP" button on this page.
2. Click on the "Download ZIP" button.
3. Save the file in a temporary folder on your PC.
4. Extract the files in the downloaded zip file.
5. Copy all the files into your Monarch/Wings ~Themes\Current\Styles folder.
6. To facilitate working with Sass, install the Microsoft "Web Essentials" package for Visual Studio 2013 from here: 
   https://visualstudiogallery.msdn.microsoft.com/56633663-6799-41d7-9df7-0f2a504ca361

Notice that all the files in this repository have the extension `.scss`. This is the extension that identifies the file as Sass (Syntactically Awesome Cascasing Style Sheet). Note also that most of the files start with `_` (underscore). `scss` files that DO NOT start with `_` (underscore) will produce automatically a `css` file with same name. In addition, a `.min.css` file is created by the Sass compiler, with an efficient (compact) version of the corresponding `css` file.
For more information on Sass, please refer to http://sass-lang.com

## Usage

If the installation is complete, your folder ~Themes\Current\Styles will have a new `Framework.css`, `Framework.min.css`, `Theme.css` and `Theme.min.css` files.

Locate the file '_config.scss` in the ~Themes\Current\Styles folder.

This file lists a series of constants used by the CSS class definitions in all the Wings-Sass project. Each of the constants starts with the symbol `$`, and define a CSS attribute. For example:

`$dds-field-error-background-color: #c00;`

One of the CSS classes that uses that constant, is:


```
.DdsCharField_Error {
    @extend .DdsCharField;
    color: $dds-field-error-color;
    background-color: $dds-field-error-background-color;
}
```

Other CSS classes defined in this project share that constant. 

To customize your Framework.css and Theme.css, change the value associated with the constants, as soon as you save the _config.scss, you can verify that the resulting `Framework.css`, `Framework.min.css`, `Theme.css` and `Theme.min.css` files are automatically updated.

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

### Removing unused CSS Styles to Optimize response time.

Let's assume that after completing your Monarch/Wings website, reight before testing, you have determined that 5250 Terminal support is not needed.

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
