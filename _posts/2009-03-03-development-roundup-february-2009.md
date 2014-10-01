---
layout: post
title: "Development roundup: February 2009"
---
Welcome to the second instalment in our monthly series of development roundup blog posts. February was a much busier month for us than January, with quite a few major changes, and over 280 commits made to our git repository.

One of the most major changes made during February was the moving of the main DMDirc UI to its own plugin. This enables us to update the UI independently of the client, and in the future will result in smaller downloads when updating either the client or the UI. We also took the opportunity to upgrade MiG Layout, the layout library used by the Swing UI, to the latest version, and now include it in our repository as a .jar rather than extracted in source code form. This makes our source tree much tidier, makes it easier for us to update to new versions in the future, and means we can now bundle the library with our UI plugin instead of the client itself.

The next large change we made was a partial revamp of the plugin system. Plugins can (and should!) now use DMDirc-style configuration files (such as those used for actions, in themes, and of course by the config system). We also introduced a system of 'services' to plugins, aimed at improving how plugins worked together and decoupling plugins from one another. Plugins can now define which services they provide (both to the user, and to other plugins), such as status bar applets, nowplaying media sources, or ways to interact with the user's computer (such as the dcop plugin); they can also require certain services be loaded, so plugins written for the Swing UI can require that the 'swing ui' service is provided for it.

With these plugin changes, we also gave plugins a way to declare certain methods for 'export' to other plugins. For example, the dcop plugin now exports its getDcopResult method under the alias 'dcop', and the dcop media source plugin requires a plugin which can provide this export. If an alternate dcop plugin is written, the dcop media source plugin could work with it right out of the box. In the future we hope to use this method for the nowplaying plugin's media sources, and perhaps even the user interface plugins.

Still on the subject of plugins, we also introduced 'subplugins' this month. Sub-plugins allow a 'child' plugin to access classes defined by the 'parent' plugin. Previously, the only way to accomplish this was to make the parent plugin persistent, which meant that it was not possible to unload or reload it. Defining this relationship formally also allows us to present it to the user when we upgrade the plugins panel in the preferences dialog (slated for 0.6.3 — watch this space).

There have also been several major back-end changes, the effects of which won't be immediately obvious to users. These are the conclusion of the command parser changes and a slight redesign of the configuration system. The former allows for more flexibility in how we assign commands, makes the processing of some commands more efficient, and fixes some issues we had when splitting command input into arguments. The configuration changes now mean that the defaults for all DMDirc settings are specified in a configuration file; previously, developers could either add them to the file or specify the default as a fallback option when they requested the setting (or both!). This change means that all settings are now listed and tab-completable with the /set command, and means that we no longer have to hunt down every use of the setting when updating defaults.

As mentioned in last month's roundup, we've been putting the finishing touches to our reworked preferences dialog. Users of nightly builds will have noticed that it now opens near-instantaneously, and does the heavy work of loading categories in the background. Another long-running project which landed this month is an improvement to the textpane designed to reduce memory usage and pave the way for more features (such as being able to copy control codes) in the future. Finally, we finished enhancing our support for SSL-enabled servers; DMDirc is now capable of validating the SSL certificate used by servers, and presents the user with a dialog if there are problems.

This month there were 67 issues resolved, so unlike last month we won't be including a list in this blog post. Anyone interested can browse the full list on our bug tracker, <a href="http://bugs.dmdirc.com/search.php?project_id=1&status_id=80&sticky_issues=on&sortby=last_updated&dir=DESC&hide_status_id=80&filter_by_date=on&start_day=1&end_day=31&start_month=2&end_month=2&start_year=2009&end_year=2009">here</a>. See you next month!

You can try out the latest developments in DMDirc before the next release by using nightly builds, available <a href="http://www.dmdirc.com/nightly">from the main website</a>. Be warned that nightly builds aren't tested extensively, and may be quite horribly broken. Finally, as always, we're happy to receive feedback or to help out with problems; the easiest way to find us is to drop by <a href="irc://irc.quakenet.org/dmdirc">#DMDirc on Quakenet</a> (which you can get to easily by using the 'Help' → 'Join dev channel' menu option in DMDirc).