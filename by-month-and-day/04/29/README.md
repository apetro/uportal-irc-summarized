Summarizes the Tuesday [April 29 2014 log][] of `#jasig-uportal` IRC chat.

uPortal 4.1 RC 1 timing
-----------------------

The UW-Madison team has a Story to cut uPortal 4.1 RC1 during this two-week sprint.

Desire for a virtual meeting post-RC and before the Apereo conference to talk through what stands in the way of a GA release.


Portlet publication permissions at the granularity of portlet types
-------------------------------------------------------------------

Discussion of what to name the new permission to publish a portlet type (takes as its target a PORTLET_TYPE as in feed reader or calendar portlet or open-ended JSR-286 portlet publication) ([UP-4064][]), with consensus on `SELECT_PORTLET_TYPE`.  This parallels somewhat the concept of permission to "SELECT" groups as targets in other contexts (as in, what groups is one permitted to select as the audience for a portlet publication or for a fragment publication) -- but I'm pretty sure that permission (to select groups as targets) doesn't exist as a real thing in modern uPortal -- it's collapsed into the permission to `VIEW` a group.

Discussion without resolution of what effect if any this permission ought to have on users managing existing portlet publications (`MANAGE`).  Can one edit a publication of a portlet that uses a portlet type that you're not permitted to select de novo?  If yes, this creates a back door to circumvent what was probably the intent of denying someone `SELECT_PORTLET_TYPE`, since the user can re-configure the instance of the type that he can manage to do whatever nefarious thing was being blocked by denying access to that portlet type.  If no, then one might have `MANAGE` or `MANAGE_*` on a category or portlet that one is not able to actually manage because of its type, and so the `MANAGE` permission in those instances becomes confusing for its lack of effect.  (Reconciling this is backlogged as [UP-4079][]).

This [changeset][changeset broke initdb] broke `ant clean initportal` by introducing a dependency of the portlet type permission target on the portlet types, but the portlet types were not reliably loaded at the time of initializing the permission target.  The change was [reverted][reverted portlet type as permission target
] to un-break the build and then re-introduced with less eager initialization.


Preferring CDNs over ResourceServer
-----------------------------------

Discussion of advantages in relying on well-regarded CDNs for common JavaScript, etc., dependencies rather than continuing to put these into ResourceServer.  `uportal-dev@` [email thread][email thread re CDNs vs ResourceServer] sprung from this discussion.


When portlets not visible to end users nonetheless count as a render in statistics
------------------

Sidebar has the behavior that portlets in the sidebar, even when not visible to the end user because the user hasn't opened the sidebar, nonetheless [count as rendered][portlets in sidebar count as rendered even if not visible] for statistics purposes since the markup rendered and then was hidden client-side.

Favorites and favorites collections do not have this behavior since the actual favorite portlets and favorite collections of portlets do not render unless the user navigates to them.


Marketplace refactor to make room for a servlet view
----------------------------------------------------

Discussion of [repackaging the guts of Marketplace][] into `org.jasig.portal.portlet.marketplace` to recognize that it's more part of uPortal's customized portlet container than anything else.



[April 29 2014 log]: http://echelog.com/logs/browse/jasig-uportal/1398722400

[UP-4064]: https://issues.jasig.org/browse/UP-4064
[UP-4079]: https://issues.jasig.org/browse/UP-4079
[changeset broke initdb]: https://github.com/Jasig/uPortal/commit/f030680f1a301ce7848f56ec82578d35535735f7
[reverted portlet type as permission target]: https://github.com/Jasig/uPortal/pull/311

[email thread re CDNs vs ResourceServer]: http://jasig.275507.n4.nabble.com/Using-CDN-vs-Resource-Server-td4662767.html

[portlets in sidebar count as rendered even if not visible]: https://github.com/jameswennmacher/uPortal/commit/e817ab2c5420dd87c42c5baab33c7f8e4b5e43b3#commitcomment-6151437

[repackaging the guts of marketplace]: https://github.com/Jasig/uPortal/pull/310
