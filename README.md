# Firefox Auto Hide Tab Bar

By Morgan Aldridge <morgant@makkintosshu.com>

## OVERVIEW

This addresses an annoyance with modern browsers run in environments which provide window decorations (e.g. title and min/max/close buttons), especially Firefox: the tab bar is always visible, even when only viewing a single tab, taking up unnecessary vertical screen real estate and repeating the window title. This automatically shows/hides the entire tab bar (including buttons) depending on the number of tabs.

* Hides tab bar when only one tab is open, including:
    * The tab, itself
    * The new tab button
    * The all tabs button/menu
    * 'Private' mode indicator
    * Moves window controls (min/max/close buttons) into the toolbar, if Firefox windows are using [client-side decorations (CSD)](https://en.wikipedia.org/wiki/Client-side_decoration)
* Shows the tab bar when there are multiple tabs open
* When the tab bar is hidden, one can still open a new tab from the Firefox main menu or via keyboard shortcuts

Unfortunately, this is not possible to implement as an extension in Firefox, only through `userChrome.css`. See installation instructions below.

## IMPLEMENTATION

This is based on an example provided in [this comment on Reddit r/firefox](https://www.reddit.com/r/firefox/comments/1h3l8sf/comment/m00a26w/), plus a trick to preserve window controls from [this comment on an irvinm/Toggle-Native-Tab-Bar GitHub issue](https://github.com/irvinm/Toggle-Native-Tab-Bar/issues/3#issuecomment-2556331029). It is implemented as a separate `auto-hide-tab-bar.css` file which can be imported into your `userChrome.css` for easier and safer integration with other customizations.

**NOTE:** This _does not_ show the window/tab title, unlike some alternatives linked below. This is because I run a window manager which provides window controls ([MLVWM](https://github.com/morgant/mlvwm), specifically), so the title is already displayed and therefore redundant. I also disable [client-side decorations (CSD)](https://en.wikipedia.org/wiki/Client-side_decoration), but have implemented moving window controls in case CSD ever gets re-enabled or I use it under another OS. 

## INSTALLATION

1. In Firefox:
    1. Enable `userChrome.css` support:
        1. Visit `about:config`
        2. Search for the `toolkit.legacyUserProfileCustomizations.stylesheets` setting
        3. Set it to `true`
    2. Locate your Firefox profile directory:
        1. Visit `about:profiles`:
        2. Look for the profile with "This is the profile in use and it cannot be deleted"
        3. Note the "Root Directory" path (**NOT** the "Local Directory") for use in the next step
2. Create `chrome/userChrome.css` in your local profile directory:
    1. Navigate to the profile's "Root Directory", as located above (e.g. `cd ~/.mozilla/<profile-root-dir>`)
    2. Create a new `chrome` subdirectory and navigate into it (e.g. `mkdir chrome && cd chrome`)
    3. Make a new `userChrome.css` file (e.g. `touch userChrome.css`)
3. Install `chrome/auto-hide-tab-bar.css`:
    1. Copy the `chrome/auto-hide-tab-bar.css` file from this repository into your profile's `chrome` subdirectory
    2. Edit the `userChrome.css` in your profile's `chrome` subdirectory to add the following line:  
        ```
        @import "./auto-hide-tab-bar.css";
        ```
4. Restart Firefox (`userChrome.css` is only loaded when Firefox launches)

## ALTERNATIVES

* [firefox-hide-tabs](https://github.com/geoffreytools/firefox-hide-tabs)
* [Toggle Native Tab Bar](https://github.com/irvinm/Toggle-Native-Tab-Bar)

## LICENSE

Released under the [MIT License](LICENSE).
