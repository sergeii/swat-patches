
Master Server Patch
===================

Description
===========
This patch will bring the vanilla server browser to life with help of swat4stats.com

.. image:: https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/screenshots/serverbrowser.png

How to install it?
==================
1. Backup the original ``Engine.dll``. This would be ``Content/System/Engine.dll`` (or ``ContentExpansion/System/Engine.dll`` if you are patching the TSS version)
2. Download the ``Engine.dll`` file corresponding to your game version

   * `SWAT 4 1.0 <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/1.0/Engine.dll>`_
   * `SWAT 4 1.1 <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/1.1/Engine.dll>`_
   * `SWAT 4: The Stetchkov Syndicate <https://raw.githubusercontent.com/sergeii/swat-patches/master/swat4stats-masterserver/TSS/Engine.dll>`_

3. Replace the original ``Engine.dll`` with the downloaded file

How to uninstall it?
====================
Replace the patched ``Engine.dll`` with the backed up one. This is it.

What does this patch do?
========================

The patched ``Engine.dll`` forces your server browser to fetch server list from swat4stats.com rather than the malfunctioning gamespy.com master server::

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


Alternative Way
===============
Perhaps this is the most convenient way to achieve the desired effect because you don't have to touch the game files at all or do it multiple times for multiple versions of the game.

Simply add these lines to your `hosts <https://support.rackspace.com/how-to/modify-your-hosts-file/>`_ file::

    62.210.142.5 swat4.available.gamespy.com
    62.210.142.5 swat4.master.gamespy.com
    62.210.142.5 swat4.ms15.gamespy.com
