
Master Server Patch
===================

Description
===========
This patch brings the server browser to life with help of master server powered by `swat4stats.com <https://swat4stats.com>`_

.. image:: https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/screenshots/serverbrowser.png

How to install this patch?
==========================

1. Download the ``Engine.dll`` file corresponding to your game version:

   .. list-table::
      :widths: 15 40 10
      :header-rows: 1

      * - SWAT 4 version
        - File location
        - Patch

      * - SWAT 4: 1.0
        - ``<SWAT 4 Path>/Content/System/Engine.dll``
        - `Download <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/1.0/Engine.dll>`_

      * - SWAT 4: 1.1
        - ``<SWAT 4 Path>/Content/System/Engine.dll``
        - `Download <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/1.1/Engine.dll>`_

      * - SWAT 4: The Stetchkov Syndicate
        - ``<SWAT 4 Path>/ContentExpansion/System/Engine.dll``
        - `Download <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/TSS/Engine.dll>`_

      * - SWAT 4: Gold Edition
        - ``<SWAT 4 Path>/Content/System/Engine.dll``

          ``<SWAT 4 Path>/ContentExpansion/System/Engine.dll``

          If you are a proud owner of the `SWAT 4: Gold Edition <https://www.gog.com/game/swat_4_gold_edition>`_ by GOG.com,
          the ``SWAT 4 Path`` would be ``C:\Program Files (x86)\GOG Galaxy\Games\SWAT 4``

        - `Content/System patch <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/1.1/Engine.dll>`_

          `ContentExpansion/System patch <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/TSS/Engine.dll>`_

2. Backup the original ``Engine.dll`` files to a safe place.
3. Replace the original ``Engine.dll`` with the downloaded file(s).

How to uninstall it?
====================
Replace the patched ``Engine.dll`` with the backed up one. This is it.


Hosting a server
================
This patch makes your server instantly appear both in `swat4stats.com/servers <https://swat4stats.com/servers/>`_ and the ingame server browser.

Before installing this patch on the server side:

* Ensure ``bLAN`` is set to ``False`` in ``SwatGUIState.ini``:
  ::

      [SwatGame.ServerSettings]
      GameType=MPM_BarricadedSuspects
      ServerName=Swat4 Server
      Password=
      bPassworded=False
      bLAN=False

  For a ``The Stetchkov Syndicate`` server, also change ``bUseStatTracking`` to ``False``:

  ::

      [SwatGame.ServerSettings]
      GameType=MPM_BarricadedSuspects
      ServerName=Swat4 Server
      Password=
      bPassworded=False
      bLAN=False
      ...
      bUseStatTracking=False

* Ensure the line ``ServerActors=IpDrv.MasterServerUplink`` is present under the section ``[Engine.GameEngine]``
  in ``Swat4DedicatedServer.ini/`` (or ``Swat4XDedicatedServer.ini`` if you're hosting a TSS server):
  ::

      [Engine.GameEngine]
      EnableDevTools=False
      InitialMenuClass=SwatGui.SwatMainMenu
      HUDMenuClass=SwatGui.HUDPage
      CacheSizeMegs=32
      UseSound=True
      ServerActors=IpDrv.MasterServerUplink

* Disable any mods (or reconfigure their listen ports) that may clash with the port range 10481-10483
  (or ``join port`` +1 - ``join port`` +3 if your server has a non default join port):

  * AMMod.AMServerQuery
  * `GS1 <https://github.com/sergeii/swat-gs1>`_
  * `GS2 <https://github.com/sergeii/swat-gs2>`_

* If the server is listed at `gametracker <http://www.gametracker.com/search/swat4/>`_ you have to change the query port to ``10481`` (or ``join port`` +1 if your server has a nondefault ``join port``)

  .. image:: https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/screenshots/gametracker.png

What does this patch do?
========================

The patched ``Engine.dll`` makes your server browser to fetch server list from swat4stats.com rather than the malfunctioning gamespy.com master server::

    < 0051e090  69 61 6d 00 00 00 00 00  25 73 2e 61 76 61 69 6c  |iam.....%s.avail|
    < 0051e0a0  61 62 6c 65 2e 67 61 6d  65 73 70 79 2e 63 6f 6d  |able.gamespy.com|
    ---
    > 0051e090  69 61 6d 00 00 00 00 00  61 76 61 69 6c 61 62 6c  |iam.....availabl|
    > 0051e0a0  65 2e 73 77 61 74 34 73  74 61 74 73 2e 63 6f 6d  |e.swat4stats.com|

    < 0051e3c0  2e 31 00 00 00 00 00 00  25 73 2e 6d 61 73 74 65  |.1......%s.maste|
    < 0051e3d0  72 2e 67 61 6d 65 73 70  79 2e 63 6f 6d 00 00 00  |r.gamespy.com...|
    ---
    > 0051e3c0  2e 31 00 00 00 00 00 00  6d 61 73 74 65 72 2e 73  |.1......master.s|
    > 0051e3d0  77 61 74 34 73 74 61 74  73 2e 63 6f 6d 00 00 00  |wat4stats.com...|

    < 0051e840  72 6f 72 3a 20 00 00 00  25 73 2e 6d 73 25 64 2e  |ror: ...%s.ms%d.|
    < 0051e850  67 61 6d 65 73 70 79 2e  63 6f 6d 00 00 00 00 00  |gamespy.com.....|
    ---
    > 0051e840  72 6f 72 3a 20 00 00 00  6d 73 25 64 2e 73 77 61  |ror: ...ms%d.swa|
    > 0051e850  74 34 73 74 61 74 73 2e  63 6f 6d 00 00 00 00 00  |t4stats.com.....|


Public server patch
===================
In addition ``Engine.dll`` contains the so called public server patch that disables validation of CD keys.
This is essential for letting players to join your server since no cd key can be validated due to gamespy shutdown in 2013.

The authorship of the public server patch belongs to:

* 1.0 - COREiSO
* 1.1 - VITALITY
* The Stetchkov Syndicate - JURAI
