# viewR

## A pipe-friendly way to invoke the `View()` function

Are you a fan of both `magrittr` pipes *and* the RStudio data viewer? Especially when doing EDA, you'll oftentimes want to casually view the current "state" of your transformed data frame without assigning it to a variable each time. (In the latter case you'd also need to select the variable and press <kbd>F2</kbd>, or <kbd>CMD</kbd> + Click on it in the Source Editor, or click on it the Environment pane.)

With `viewR`, you can seamlessly view the currently selected lines of code in the RStudio data viewer: Simply select the lines (just as you always would) and then, instead of executing them (which will print the result to the console and may be undesirable for formatting reasons), you can assign an RStudio shortcut to `view_selection` (the workhorse of `viewR`) and immediately view the current selection in the data viewer, all while keeping your hands on the keyboard. The title of the new data tab is inferred from the first element in the chain and suffixed with a `_view`.

You can even keep the trailing `%>%` selected, making it easy to keyboard-navigate through your code and seamlessly invoke `viewR` on "mid-code" selections without any intermediate steps.

## Demo

![](viewr_demo.gif)

## Installation

Install `viewR` from GitHub with

```r
# install.packages("devtools")
devtools::install_github("lukasfeick-sw/viewR")
```

## Recommended use

`viewR` unfolds its full potential when it's mapped to a sensible keyboard shortcut, for example <kbd>CMD</kbd> + <kbd>Shift</kbd> + <kbd>V</kbd> (as in *V*iew). As for the source code, the necessary infrastructure for this is already in place: In RStudio, navigate to 'Tools' > 'Modify Keyboard Shortcuts' and then search for 'View current selection'. Click on the 'Shortcut' field to assign a new keyboard shortcut.

## Backend

The [backend](https://github.com/lukasfeick-sw/viewR/blob/master/R/view_selection.R) is, really, as simple as it gets: `view_selection` relies heavily on the [`rstudioapi`](https://github.com/rstudio/rstudioapi) package. It captures the currently selected lines, cleans them up, extracts the title to be used for the Viewer tab, adds a `View()` call at the end and then sends the result to the console where it's executed, invoking the data viewer.

