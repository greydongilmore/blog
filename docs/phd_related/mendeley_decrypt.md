---
title: How to extract data from an encryted Mendeley database
template: overrides/main.html
---

In an effort to stop users from porting their databases to other software like Zotero, Mendeley has begun encrypting the user database. Mendeley is using the SQLite Encryption Extension (“SEE”) with a hidden key. The SEE library is closed-source and very proprietary. Its API is documented, but its on-disk structures are not (publicly) documented, and the source code is not publicly available. Applications using SEE are required to make it impossible to access SEE functionality from outside the application.

## Prep

This method is working on Linux (Ubuntu 20.04 and Pop!_OS 20.04).

You will need to install:

* gdm: `sudo apt-get install -y gdm`

Mendeley should be installed in either two ways:

* Flatpak app
* from a `.deb` file

## Extract your data

1. Make sure you quit Mendeley before proceeding.
2. Locate your Mendeley database, the database is usually found in either:

    * `~/.local/share/data/Mendeley\ Ltd./Mendeley\ Desktop/`
    * `~/.var/app/com.elsevier.MendeleyDesktop/data/data/Mendeley\ Ltd./Mendeley\ Desktop/`

    You will find several sqlite databases:

    * **<user_id>@www.mendeley.com.sqlite** <--this is the one we want
    * <user_id>@www.mendeley.com.sqlite-wal
    * <user_id>@www.mendeley.com.sqlite-shm
    * <user_id>-monitor.sqlite
    * <user_id>-monitor.sqlite-wal
    * <user_id>-monitor.sqlite-shm

3. Make a backup copy of the encrypted database. In my case, I installed Mendeley as a Flatpak app so I ran the following to make a backup copy:

    ```console
    cd ~/.var/app/com.elsevier.MendeleyDesktop/data/data/Mendeley\ Ltd./Mendeley\ Desktop/
    cp 579d4e70-4479-3965-8590-1ddf5803d0c1@www.mendeley.com.sqlite ~/backup-encrypted.sqlite
    ```

4. You will now run Mendeley in debug mode, depending on how you installed it:
    
    a. if you installed with a `.deb` package, debug using `gdb` directly:

    ```console
    mendeleydesktop --debug
    ```

    b. if you installed with Flatpak, you need to run with Flatpak first then `gdb`:

    ```console
    # Run with Flatpak
    $ flatpak run --devel --command=sh com.elsevier.MendeleyDesktop

    # Run gdb within the Flatpak sandbox
    [📦 com.elsevier.MendeleyDesktop ~]$ QT_QPA_PLATFORM_PLUGIN_PATH=/app/extra/plugins/qt/plugins/platforms/ gdb --args /app/extra/bin/mendeleydesktop

    ```

5. Add a breakpoint that captures the moment a SQLite database is opened:

    ```console
    (gdb) b sqlite3_open_v2
    ```

6. Start the program now:

    ```console
    (gdb) run
    ```

7. The program will stop at the breakpoint several times. Keep continuing the program until the string pointed to by `$rdi` names the file you backed up in the step above (press `c` to continue and enter `x/s $rdi` to check the filename):

    ```console
    # Run x/s $rdi and look at the filename
    Thread 1 "mendeleydesktop" hit Breakpoint 1, 0x000000000101b1b0 in sqlite3_open_v2 ()
    (gdb) x/s $rdi
    0x1dca928:	"~/.var/app/com.elsevier.MendeleyDesktop/share/data/data/Mendeley Ltd./Mendeley Desktop/Settings.sqlite"

    # Enter c to continue
    (gdb) c
    Continuing.

    Thread 1 "mendeleydesktop" hit Breakpoint 1, 0x000000000101b1b0 in sqlite3_open_v2 ()
    (gdb) x/s $rdi
    0x1dcb318:	"~/.var/app/com.elsevier.MendeleyDesktop/share/data/data/Mendeley Ltd./Mendeley Desktop/Settings.sqlite"
    (gdb) c

    # Keep repeating the above until you find the .sqlite file that you backed up earlier
    Thread 1 "mendeleydesktop" hit Breakpoint 1, 0x000000000101b1b0 in sqlite3_open_v2 ()
    (gdb) x/s $rdi
    0x25f1818:	"~/.var/app/com.elsevier.MendeleyDesktop/share/data/data/Mendeley Ltd./Mendeley Desktop/579d4e70-4479-3965-8590-1ddf5803d0c1@www.mendeley.com.sqlite"
    ```

8. You will need to continue (`c`) until you see the same database filename appear again (`x/s $rdi`), usually happens immediately after the first appearance.

9. Now, set a breakpoint for the moment the key is supplied to SQLite Encryption Extension by using `b sqlite3_key`:

    ```console
    # Set a new breakpoint
    (gdb) b sqlite3_key
    Breakpoint 2 at 0x101b2c0

    # Press c to continue
    (gdb) c
    Continuing.
    ```

10. When the subsequent breakpoint is hit, enter `info registers` to determine the value of `rdi`:

    ```console
    # When the breakpoint is hit, run `info registers`
    Thread 1 "mendeleydesktop" hit Breakpoint 2, 0x000000000101b2c0 in sqlite3_key ()
    (gdb) info registers 
    rax            0x7fffffffc6b0	  140737488340656
    rbx            0x25f0590	      39781776
    rcx            0x7fffea9a0c40	  140737129352256
    rdx            0x20	            32
    rsi            0x260fd68	      39910760
    rdi            0x25ef4e8	      39777512
    rbp            0x7fffffffc730	  0x7fffffffc730
    rsp            0x7fffffffc688	  0x7fffffffc688
    r8             0xc1	            193
    r9             0x7fffea9a0cc0	  140737129352384
    r10            0x0	            0
    r11            0x1	            1
    r12            0x7fffffffc6b0	  140737488340656
    r13            0x7fffffffc6a0	  140737488340640
    r14            0x7fffffffc790	  140737488340880
    r15            0x7fffffffc790	  140737488340880
    rip            0x101b2c0	      0x101b2c0 <sqlite3_key>
    eflags         0x202	          [ IF ]
    cs             0x33	            51
    ss             0x2b	            43
    ds             0x0	            0
    es             0x0	            0
    fs             0x0	            0
    gs             0x0	            0
    ```

11. Copy down the value of `rdi` from the second column of the `info registers` output. It is the pointer to the open SQLite database handle. Then, finish execution of sqlite3_key by running `fin`.

    ```console
    (gdb) fin
    Run till exit from #0  0x000000000101b2c0 in sqlite3_key ()
    0x0000000000f94e54 in SqliteDatabase::openInternal(QString const&, SqlDatabaseKey*) ()
    ```

12. Use gdb’s ability to call C functions to `rekey` the database to the null key, thereby decrypting it in-place and allowing export of the SQL data:

    ```console
    (gdb) p (int) sqlite3_rekey_v2(0x25ef4e8, 0, 0, 0)
    $1 = 0
    ```

13. If you see `$1 = 0` from the `rekey` command then you are ready to export the SQL data (step 14), if you see `$1 = 8` then you need to follow the below steps.
    * Mendeley will sometimes re-open the database a few times during startup sp this may  have caused the error
    * To work around the random opening of the database, check if the program opens the main database a second time 
    * Run step 7-8 again up to the `p sqlite3_rekey_v2(...)` step, but do not run `sqlite3_rekey_v2`
    * Instead, just type `c` to continue, returning to the step where you inspect each call to `sqlite3_open_v2`, waiting for one with `$rdi` pointing to a string with the right database filename. When you see it come round again, then try the `sqlite3_rekey_v2` step
    * If you see `$1 = 0` this time, you’re all set, and can proceed as described above for a successful call to `sqlite3_rekey_v2`

14. Once the database is decrypted it is a good idea to save a copy of the database to a new location:

    ```console
    cd ~/.var/app/com.elsevier.MendeleyDesktop/data/data/Mendeley\ Ltd./Mendeley\ Desktop/
    cp 579d4e70-4479-3965-8590-1ddf5803d0c1@www.mendeley.com.sqlite ~/backup-decrypted.sqlite
    ```

15. Now you can quit `gbd`:

    ```console
    (gdb) quit
    A debugging session is active.

        Inferior 1 [process 32750] will be killed.

    Quit anyway? (y or n) y
    [322:322:0100/000000.491674:ERROR:broker_posix.cc(43)] Invalid node channel message
    ```

    if also running `Flatpak`:

    ```console
    [📦 com.elsevier.MendeleyDesktop ~]$ exit
    ```

16. Lastly, restore your backup copy of the encrypted database, so that Mendeley will continue to run OK:

    ```console
    cd ~/.var/app/com.elsevier.MendeleyDesktop/data/data/Mendeley\ Ltd./Mendeley\ Desktop/
    cp ~/backup-encrypted.sqlite 579d4e70-4479-3965-8590-1ddf5803d0c1@www.mendeley.com.sqlite
    ```

17. You can now use software like [SQLite Browser](https://sqlitebrowser.org/) to open and view the database (`~/backup-decrypted.sqlite`)
