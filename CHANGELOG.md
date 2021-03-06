# 0.10.0 (2018-10-16)

## Week 10: Subscriptions

This week I'm happy to announce that subscriptions have been drastically sped up with
35e63fa. As I mentioned last week, this essentially "caches" a user's feed, meaning that operations that previously took 20 seconds or timed out, now can load in under a second. I'd take a look at [#173](https://github.com/omarroth/invidious/issues/173) for a sample benchmark. Previously features that made Invidious's feed so useful, such as filtering by unseen and by author would take too long to load, and so instead would timeout. I'm very happy that this has been fixed, and folks can get back to using these features.

Among some smaller features that have been added this week include [#118](https://github.com/omarroth/invidious/issues/118), which adds, in my opinion, some very attractive subscribe and unsubscribe buttons. I think it's also a bit of a functional improvement as well, since it doesn't require a user to reload the page in order to subscribe or unsubscribe to a channel, and also gives the opportunity to put the channel's sub count on display.

An option to swap between Reddit and YouTube comments without a page reload has been added with
5eefab6, bringing it somewhat closer in functionality to the popular [AlienTube](https://github.com/xlexi/alientube) extension, on which it is based (although the extension unfortunately appears now to be fragmented).

As always, there are a couple smaller improvements this week, including some minor fixes for geo-bypass with
e46e618 and [`245d0b5`](https://github.com/omarroth/invidious/245d0b5), playlist preferences with [`81b4477`](https://github.com/omarroth/invidious/81b4477), and YouTube comments with [`02335f3`](https://github.com/omarroth/invidious/02335f3).

This coming week I'd also recommend keeping an eye on the excellent [FreeTube](https://github.com/FreeTubeApp/FreeTube), which is looking forward to a new release. I've been very lucky to work with [**@PrestonN**](https://github.com/PrestonN) for the past few weeks to improve the Invidious API, and I'm quite looking forward to the new release.

That's all for this week folks, thank you all again for your continued interest and support.

# 0.9.0 (2018-10-08)

## Week 9: Playlists

Not as much to announce this week, but I'm still quite happy to announce a couple things, namely:

Playback support for playlists has finally been added with [`88430a6`](https://github.com/omarroth/invidious/88430a6). You can now view playlists with the `&list=` query param, as you would on YouTube. You can also view mixes with the mentioned `&list=`, although they require some extra handling that I would like to add in the coming week, as well as adding playlist looping and shuffle. I think playback support has been a roadblock for more exciting features such as [#114](https://github.com/omarroth/invidious/issues/114), and I look forward to improving the experience.

Comments have had a bit of a cosmetic upgrade with [#132](https://github.com/omarroth/invidious/issues/132), which I think helps better distinguish between Reddit and YouTube comments, as it makes them appear similarly to their respective sites. You can also now switch between YouTube and Reddit comments with a push of a button, which I think is quite an improvement, especially for newer or less popular videos with fewer comments.

I've had a small breakthrough in speeding up users' subscription feeds with PostgreSQL's [materialized views](https://www.postgresql.org/docs/current/static/rules-materializedviews.html). Without going into too much detail, materialized views essentially cache the result of a query, making it possible to run resource-intensive queries once, rather than every time a user visits their feed. In the coming week I hope to push this out to users, and hopefully close [#173](https://github.com/omarroth/invidious/issues/173).

I haven't had as much time to work on the project this week, but I'm quite happy to have added some new features. Have a great week everyone.

# 0.8.0 (2018-10-02)

## Week 8: Mixes

Hello again!

Mixes have been added with [`20130db`](https://github.com/omarroth/invidious/20130db), which makes it easy to create a playlist of related content. See [#188](https://github.com/omarroth/invidious/issues/188) for more info on how they work. Currently, they return the first 50 videos rather than a continuous feed to avoid tracking by Google/YouTube, which I think is a good trade-off between usability and privacy, and I hope other folks agree. You can create mixes by adding `RD` to the beginning of a video ID, an example is provided [here](https://www.invidio.us/mix?list=RDYE7VzlLtp-4) based on Big Buck Bunny. I've been quite happy with the results returned for the mixes I've tried, and it is not limited to music, which I think is a big plus. To emulate a continuous feed provided many are used to, using the last video of each mix as a new 'seed' has worked well for me. In the coming week I'd like to to add playback support in the player to listen to these easily.

A very big thanks to [**@flourgaz**](https://github.com/flourgaz) for Docker support with [#186](https://github.com/omarroth/invidious/pull/186). This is an enormous improvement in portability for the project, and opens the door for Heroku support (see [#162](https://github.com/omarroth/invidious/issues/162)), and seamless support on Windows. For most users, it should be as easy as running `docker-compose up`.

I've spent quite a bit of time this past week improving support for geo-bypass (see [#92](https://github.com/omarroth/invidious/issues/92)), and am happy to note that Invidious has been able to proxy ~50% of the geo-restricted videos I've tried. In addition, you can now watch geo-restricted videos if you have `dash` enabled as your `preferred quality`, for more details see [#34](https://github.com/omarroth/invidious/issues/34) and [#185](https://github.com/omarroth/invidious/issues/185), or last week's update. For folks interested in replicating these results for themselves, I'd take a look [here](https://gist.github.com/omarroth/3ce0f276c43e0c4b13e7d9cd35524688) for the script used, and [here](https://gist.github.com/omarroth/beffc4a76a7b82a422e1b36a571878ef) for a list of videos restricted in the US.

1080p has seen a fairly smooth roll-out, although there have been a couple issues reported, mainly [#193](https://github.com/omarroth/invidious/issues/193), which is likely an issue in the player. I've also encountered a couple other issues myself that I would like to investigate. Although none are major, I'd like to keep 1080p opt-in for registered users another week to better address these issues.

Have an excellent week everyone.

# 0.7.0 (2018-09-25)

## Week 7: 1080p and Search Types

Hello again everyone! I've got quite a couple announcements this week:

Experimental 1080p support has been added with [`b3ca392`](https://github.com/omarroth/invidious/b3ca392), and can be enabled by going to preferences and changing `preferred video quality` to `dash`. You can find more details [here](https://github.com/omarroth/invidious/issues/34#issuecomment-424171888). Currently quality and speed controls have not yet been integrated into the player, but I'd still appreciate feedback, mainly on any issues with buffering or DASH playback. I hope to integrate 1080p support into the player and push support site-wide in the coming weeks.

You can now filter content types in search with the `type:TYPE` filter. Supported content types are `playlist`, `channel`, and `video`. More info is available [here](https://github.com/omarroth/invidious/issues/126#issuecomment-423823148). I think this is quite an improvement in usability and I hope others find the same.

A [CHANGELOG](https://github.com/omarroth/invidious/blob/master/CHANGELOG.md) has been added to the repository, so folks will now receive a copy of all these updates when cloning. I think this is an improvement in hosting the project, as it is no longer tied to the `/releases` tab on Github or the posts on Patreon.

Recently, users have been reporting 504s when attempting to access their subscriptions, which is tracked in [#173](https://github.com/omarroth/invidious/issues/173). This is most likely caused by an uptick in usage, which I am absolutely grateful for, but unfortunately has resulted in an increase in costs for hosting the site, which is why I will be bumping my goal on Patreon from $60 to $80. I would appreciate any feedback on how subscriptions could be improved.

Other minor improvements include:

- Additional regions added to bypass geo-block with [`9a78523`](https://github.com/omarroth/invidious/9a78523)
- Fix for playlists containing less than 100 videos (previously shown as empty) with [`35ac887`](https://github.com/omarroth/invidious/35ac887)
- Fix for `published` date for Reddit comments (previously showing negative seconds) with [`6e09202`](https://github.com/omarroth/invidious/6e09202)

Thank you everyone for your support!

# 0.6.0 (2018-09-18)

## Week 6: Filters and Thumbnails

Hello again! This week I'm happy to mention a couple new features to search as well as some miscellaneous usability improvements.

You can now constrain your search query to a specific channel with the `channel:CHANNEL` filter (see [#165](https://github.com/omarroth/invidious/issues/165) for more details). Unfortunately, other search filters combined with channel search are not yet supported. I hope to add support for them in the coming weeks.

You can also now search only your subscriptions by adding `subscriptions:true` to your query (see [#30](https://github.com/omarroth/invidious/issues/30) for more details). It's not quite ready for widespread use but I would appreciate feedback as the site updates to fully support it. Other search filters are not yet supported with `subscriptions:true`, but I hope to add more functionality to this as well.

With [#153](https://github.com/omarroth/invidious/issues/153) and [#168](https://github.com/omarroth/invidious/issues/168) all images on the site are now proxied through Invidious. In addition to offering the user more protection from Google's eyes, it also allows the site to automatically pick out the highest resolution thumbnail for videos. I think this is quite a large aesthetic improvement and I hope others will find the same.

As a smaller improvement to the site, you can also now view RSS feeds for playlists with [#113](https://github.com/omarroth/invidious/issues/113).

These updates are also now listed under Github's [releases](https://github.com/omarroth/invidious/releases). I'm also planning on adding them as a `CHANGELOG.md` in the repository itself so people can receive a copy with the project's source.

That's all for this week. Thank you everyone for your support!

# 0.5.0 (2018-09-11)

## Week 5: Privacy and Security

I hope everyone had a good weekend! This past week I've been fixing some issues that have been brought to my attention to help better protect users and help them keep their anonymity.

An issue with open referers has been fixed with [`29a2186`](https://github.com/omarroth/invidious/29a2186), which prevents potential redirects to external sites on actions such as login or modifying preferences.

Additionally, X-XSS-Protection, X-Content-Type-Options, and X-Frame-Options headers have been added with [`96234e5`](https://github.com/omarroth/invidious/96234e5), which should keep users safer while using the site.

A potential XSS vector has also been fixed in YouTube comments with [`8c45694`](https://github.com/omarroth/invidious/8c45694).

All the above vulnerabilities were brought to my attention by someone who wishes to remain anonymous, but I would like to say again here how thankful I am. If anyone else would like to get in touch please feel free to email me at omarroth@hotmail.com or omarroth@protonmail.com.

This week a couple changes have been made to better protect user's privacy as well.
All CSS and JS assets are now served locally with [`3ec684a`](https://github.com/omarroth/invidious/3ec684a), which means users no longer need to whitelist unpkg.com. Although I personally have encountered few issues, I understand that many folks would like to keep their browsing activity contained to as few parties as possible. In the coming week I also hope to proxy YouTube images, so that no user data is sent to Google.

YouTube links in comments now should redirect properly to the Invidious alternate with [`1c8bd67`](https://github.com/omarroth/invidious/1c8bd67) and [`cf63c82`](https://github.com/omarroth/invidious/cf63c82), so users can more easily evade Google tracking.

I'm also happy to mention a couple quality of life features this week:

Invidious now shows a video's "license" if provided, see [#159](https://github.com/omarroth/invidious/issues/159) for more details. You can also search for videos licensed under the creative commons with "QUERY features:creative_commons".

Videos with only one source will always display the cog for changing quality, so that users can see what quality is currently playing. See [#158](https://github.com/omarroth/invidious/issues/158) for more details.

Folks have also probably noticed that the gutters on either side of the screen have been shrunk down quite significantly, so that more of the screen is filled with content. Hopefully this can be improved even more in the coming weeks.

"Music", "Sports", and "Popular on YouTube" channels now properly display their videos. You can subscribe to these channels just as you would normally.

This coming week I'm planning on spending time with my family, so I unfortunately may not be as responsive. I do still hope to add some smaller features for next week however, and I hope to continue development soon.
Thank you everyone again for your support.

# 0.4.0 (2018-09-06)

## Week 4: Genre Channels

Hello! I hope everyone enjoyed their weekend. Without further ado:
Just today genre channels have been added with [#119](https://github.com/omarroth/invidious/issues/119). More information on genre channels is available [here](https://support.google.com/youtube/answer/2579942). You can subscribe to them as normally, and view them as RSS. I think they offer an interesting alternative way to find new content and I hope people find them useful.

This past week folks have started reporting 504s on their subscription page (see [#144](https://github.com/omarroth/invidious/issues/144) for more details). Upgrading the database server appeared to fix the issue, as well as providing a smoother experience across the site. Unfortunately, that means I will be increasing the goal from $50 to $60 in order to meet the increased hosting costs.

With [#134](https://github.com/omarroth/invidious/issues/134), comments are now formatted correctly, providing support for bold, italics, and links in comments. I think this improvement makes them much easier to read, and I hope others find the same. Also to note is that links in both comments and the video description now no longer contain any of Google's tracking with [#115](https://github.com/omarroth/invidious/issues/115).

One of the major use cases for Invidious is as a stripped-down version of YouTube. In line with that, I'm happy to announce that you can now hide related videos if you're logged in, for users that prefer an even more lightweight experience.

Finally, I'm pleased to announce that Invidious has hit 100 stars on GitHub. I am very happy that Invidious has proven to be useful to so many people, and I can't say how grateful I am to everyone for their continued support.

Enjoy the rest of your week everyone!

# 0.3.0 (2018-09-06)

## Week 3: Quality of Life

Hello everyone! This week I've been working on some smaller features that will hopefully make the site more functional.
Search filters have been added with [#126](https://github.com/omarroth/invidious/issues/126). You can now specify 'sort', 'date', 'duration', and 'features' within your query using the 'operator:value' syntax. I'd recommend taking a look [here](https://github.com/omarroth/invidious/blob/master/src/invidious/search.cr#L33-L114) for a list of supported options and at [#126](https://github.com/omarroth/invidious/issues/126) for some examples. This also opens the door for features such as [#30](https://github.com/omarroth/invidious/issues/30) which can be implemented as filters. I think advanced search is a major point in which Invidious can improve on YouTube and hope to add more features soon!

This week a more advanced system for viewing fallback comments has been added (see [#84](https://github.com/omarroth/invidious/issues/84) for more details). You can now specify a comment fallback in your preferences, which Invidious will use. If, for example, no Reddit comments are available for a given video, it can choose to fallback on YouTube comments. This also makes it possible to turn comments off completely for users that prefer a more streamlined experience.

With [#98](https://github.com/omarroth/invidious/issues/98), it is now possible for users to specify preferences without creating an account. You can now change speed, volume, subtitles, autoplay, loop, and quality using query parameters. See the issue above for more details and several examples.

I'd also like to announce that I've set up an account on [Liberapay](https://liberapay.com/omarroth), for patrons that prefer a privacy-friendly alternative to Patreon. Liberapay also does not take any percentage of donations, so I'd recommend donating some to the Liberapay for their hard work. Go check it out!

[Two weeks ago](https://github.com/omarroth/invidious/releases/tag/0.1.0) I mentioned adding 1080p support into the player. Currently, the only thing blocking is [#207](https://github.com/videojs/http-streaming/pull/207) in the excellent [http-streaming](https://github.com/videojs/http-streaming) library. I hope to work with the videojs team to merge it soon and finally implement 1080p support!

That's all for this week, thank you again everyone for your support!

# 0.2.0 (2018-09-06)

## Week 2: Toward Playlists

Sorry for the late update! Not as much to announce this week, but still a couple things of note:
I'm happy to announce that a playlists page and API endpoint has been added so you can now view playlists. Currently, you cannot watch playlists through the player, but I hope to add that in the coming week as well as adding functionality to add and modify playlists. There is a good conversation on [#114](https://github.com/omarroth/invidious/issues/114) about giving playlists even more functionality, which I think is interesting and would appreciate feedback on.

As an update to the Invidious API announcement last week, I've been working with [**@PrestonN**](https://github.com/PrestonN), the developer of [FreeTube](https://github.com/FreeTubeApp/FreeTube), to help migrate his project to the Invidious API. Because of it's increasing popularity, he has had trouble keeping under the quota set by YouTube's API. I hope to improve the API to meet his and others needs and I'd recommend folks to keep an eye on his excellent project! There is a good discussion with his thoughts [here](https://github.com/FreeTubeApp/FreeTube/issues/100).

A couple of miscellaneous features and bugfixes:

- You can now login to Invidious simultaneously from multiple devices - [#109](https://github.com/omarroth/invidious/issues/109)

- Added a note for scheduled livestreams - [#124](https://github.com/omarroth/invidious/issues/124)

- Changed YouTube comment header to "View x comments" - [#120](https://github.com/omarroth/invidious/issues/120)

Enjoy your week everyone!

# 0.1.0 (2018-09-06)

## Week 1: Invidious API and Geo-Bypass

Hello everyone! This past week there have been quite a few things worthy of mention:

I'm happy to announce the [Invidious Developer API](https://github.com/omarroth/invidious/wiki/API). The Invidious API does not use any of the official YouTube APIs, and instead crawls the site to provide a JSON interface for other developers to use. It's still under development but is already powering [CloudTube](https://github.com/cloudrac3r/cadencegq). The API currently does not have a quota (compared to YouTube) which I hope to continue thanks to continued support from my Patrons. Hopefully other developers find it useful, and I hope to continue to improve it so it can better serve the community.

Just today partial support for bypassing geo-restrictions has been added with [fada57a](https://github.com/omarroth/invidious/commit/fada57a307d66d696d9286fc943c579a3fd22de6). If a video is unblocked in one of: United States, Canada, Germany, France, Japan, Russia, or United Kingdom, then Invidious will be able to serve video info. Currently you will not yet be able to access the video files themselves, but in the coming week I hope to proxy videos so that users can enjoy content across borders.

Support for generating DASH manifests has been fixed, in the coming week I hope to integrate this functionality into the watch page, so users can view videos in 1080p and above.

Thank you everyone for your continued interest and support!
