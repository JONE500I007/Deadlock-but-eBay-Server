# Deadlock eBay - Server Kit
This kit runs the Deadlock eBay auction mode on a server on your own PC. Friends join over Steam:
no port forwarding needed.

WHAT YOU NEED
1. Windows 10/11 and Deadlock (Steam).
2. .NET Runtime 10 (x64)  https://dotnet.microsoft.com/download/dotnet/10.0
   (the setup checks it and opens the download page if it's missing)
3. Deadworks (runs Deadlock dedicated servers with plugins)  https://deadworks.net/
   The setup downloads the latest release from Deadworks' GitHub by itself (needs internet).
   If that fails: download deadworks-vX.X.X.zip from https://github.com/Deadworks-net/deadworks/releases
   and put it in this folder. (The site's "DOWNLOAD CLIENT" button is the players' launcher, not the server.)

INSTALL (first time)
1. Extract this kit anywhere, e.g. Desktop\Deadlock_eBay_ServerKit
2. Close Deadlock, then double-click  setup_server.bat
   It finds your Deadlock folder, downloads and installs Deadworks, installs the eBay plugin,
   adds the auction panel for this PC (pak92_dir.vpk, if you don't have it yet) and edits gameinfo.gi
   so friends can join over Steam (backup: gameinfo.gi.before_ebay).
   An x10 mode plugin, if present, is moved to managed\plugins_disabled (the two modes can't run together).

START AND JOIN
1. Double-click  start_ebay_server.bat  and wait until the server window has loaded the map.
2. You: start Deadlock -> Settings -> enable "Dev command console" -> press F7 and type
        connect localhost:27016
3. Friends: in the SERVER window type  status  and copy the steamid, e.g. [A:1:1234567890:12345]
   Friends press F7 and type   connect [A:1:1234567890:12345]
   (the steamid changes every time the server starts)
4. The auction panel (item icon, bid buttons, item cards) needs Deadworks' client UI on each player's PC:
   Deadlock_eBay.zip from GameBanana (mod manager, or copy pak92_dir.vpk into Deadlock\game\citadel\addons),
   or join through the Deadworks launcher. Without it you can still play: auctions show in chat, bid with /b 500.
5. The match starts like a normal match. First auction at 1:30 (all rules: README.txt).

SETTINGS
File: Deadlock\game\bin\win64\configs\EBayPlugin\EBayPlugin.jsonc (made on the first server start).
Edit it, then type  dw_reloadconfig  in the server window (no restart needed).
Settings that aren't in the file yet can be added by hand; the rest keep their defaults.

  AuctionSeconds / PauseSeconds      length of an auction / the break between two (30 / 10)
  FirstAuctionAtClock                match clock of the first auction in seconds (90 = 1:30)
  MinBid / MaxBid                    smallest bid / biggest single bid (0 = no limit)
  LoserRefundPercent                 what losers get back (50)
  SellRefundPercent                  selling an auction item gives back this % of what was paid (50)
  TierPhases                         chance of 800 / 1600 / 3200 / 6400 / Legendary items by match minute
  LegendaryEveryMinutes              a Legendary every N minutes (10, 0 = off)
  EnhancedChancePercent / CorruptedChancePercent   chance of the Enhanced / Corrupted version (25 / 25)
  ExcludedItems                      item ids that never come up
  PlayerListings, MaxListingsPerPlayer, MaxListingQueue   players selling their own items (on, 3, 12)
  NoDuplicateHeroes, LockHeroAfterPick                    each hero once, no switching after the pick
  BalanceTeams, BalanceCountsBots                         can't join the bigger team (on, bots not counted)
  ItemCardLanguage                   language of the item card on the auction icon: "english" or "thai"
  PanelBottomPx / PanelOffsetX       auction panel position (pixels from the bottom / from the centre, - = left)
  BidButtonsBottomPx / BidButtonsOffsetX, SellButtonBottomPx / SellButtonOffsetX   button positions
  BidButtons                         the bid buttons' amounts ([50, 250, 1000])

PROBLEMS
- After a Deadlock update the server won't start / friends can't join: run setup_server.bat again
  (updates Deadworks, puts the gameinfo.gi lines back) and get the latest kit.
- No auction panel: that player has no Deadworks client UI (see 4). /b 500 in chat still works.
- Back to x10 mode: in Deadlock\game\bin\win64\managed move EBayPlugin.dll from plugins to plugins_disabled
  and X10ServerPlugin.dll from plugins_disabled back to plugins, then start the server with x10's kit.
  (Back to eBay: just run start_ebay_server.bat, it switches by itself.)
- Lines starting with [ebay] in the server window are the plugin's log: send them along when reporting a bug.

Credits: Deadworks (server plugins + HUD UI, https://deadworks.net), ValveResourceFormat.
pak92_dir.vpk is Deadworks' client UI (GPLv3, see DEADWORKS_UI_LICENSE.txt).
Deadlock is a game by Valve. Unofficial fan mod.
