

### Compatible Exchanges

||with Post-Only Orders support|without Post-Only|
|---|---|---|
|**with Maker and Taker fees**|[Coinbase](https://pro.coinbase.com/) <sub>([fees](https://pro.coinbase.com/orders/fees))</sub><br> &#10239; _REST + WebSocket + FIX_<br><br>[Binance](https://www.binance.com/) <sub>([fees](https://www.binance.com/en/fee/schedule))</sub><br> &#10239; _REST + WebSocket_<br><br>[Kraken](https://www.kraken.com/) <sub>([fees](https://www.kraken.com/features/fee-schedule))</sub><br> &#10239; _REST + WebSocket²_<br><br>[KuCoin](https://www.kucoin.com/) <sub>([fees](https://www.kucoin.com/vip/level))</sub><br> &#10239; _REST + WebSocket_<br><br>[Bitfinex](https://www.bitfinex.com/) <sub>([fees](https://www.bitfinex.com/fees))</sub><br>[Ethfinex](https://www.ethfinex.com/) <sub>([fees](https://www.ethfinex.com/fees))</sub><br> &#10239; _REST + WebSocket_<br><br>[Gate.io](https://www.gate.io/) <sub>([fees](https://www.gate.io/fee))</sub><br> &#10239; _REST + WebSocket_<br><br>[HitBTC](https://hitbtc.com/) <sub>([fees](https://hitbtc.com/fee-tier))</sub><br>[Bequant](https://bequant.io/) <sub>([fees](https://bequant.io/fees-and-limits))</sub><br> &#10239; _REST + WebSocket²_<br><br>[Poloniex](https://www.poloniex.com/) <sub>([fees](https://poloniex.com/fees/))</sub><br> &#10239; _REST + WebSocket_|*none*|
|**without Maker fees**|[BitMEX](https://www.bitmex.com/) <sub>([fees](https://www.bitmex.com/app/fees))</sub><br> &#10239; _REST + WebSocket_|*none*|

All currency pairs are supported.

## README
- Documentation
  - [README](#readme)
  - [MANUAL](https://github.com/ctubio/Krypto-trading-bot/blob/master/doc/MANUAL.md)
- Installation
  - [Docker Installation](#docker-installation)
  - [Windows Installation](#windows-installation)
  - [Manual GIT Installation](#manual-git-installation)
  - [Manual ZIP Installation](#manual-zip-installation)
  - [Configuration After Manual Installation](#configuration-after-manual-installation)
  - [Upgrade to the latest commit](#upgrade-to-the-latest-commit)
  - [Multiple instances party time](#multiple-instances-party-time)
- Information
  - [Compatible Exchanges](#compatible-exchanges)
  - [Application Usage](#application-usage)
  - [Web UI](#web-ui)
  - [Databases](#databases)
  - [Charts](#charts)
  - [Cloud Hosting](#cloud-hosting)
- Development
  - [Build notes](#build-notes)
  - [Changelogs](#unreleased-changelog)
- Humans and Milk Mammals
  - [Unlock](#unlock)
  - [Donations](#donations)
  - [General Discussion](#general-discussion)
  - [Very Special Thanks](#very-special-thanks-to)
  - [Help](#help)
  - [Issues](#issues)

### Docker Installation

See [etc/Dockerfile](https://github.com/ctubio/Krypto-trading-bot/tree/master/etc#dockerfile) file.

### Windows Installation

Before proceed with a manual installation, ensure your target machine has Windows 7 or greater and [MSYS2](https://www.msys2.org/) installed.

Use MSYS2 Terminal to install `make` (with command `pacman -S make`), and then proceed as usual with the installation.

### Manual GIT Installation

0. Ensure you agree to install collaborative non-free software (see [Unlock](#unlock) section).

1. Ensure your target machine has `git` and `make` installed.

2. Download it wherever you want (feel free to customize the suggested folder name K) and execute the installer:
```
 $ git clone ssh://git@github.com/ctubio/Krypto-trading-bot K
 $ cd K
 $ make install
```

3. Open and edit the config file `K.sh` in your favorite text editor:
```
 $ vim K.sh
```

To upgrade anytime see [Upgrade to the latest commit](#upgrade-to-the-latest-commit) section.

### Manual ZIP Installation

0. Ensure you agree to install collaborative non-free software (see [Unlock](#unlock) section).

1. Ensure your target machine has `curl` and `make` installed.

2. Download it wherever you want (feel free to customize the suggested folder name K) and execute the installer:
```
 $ mkdir K
 $ cd K
 $ curl -O krypto.ninja/Makefile
 $ make install
```

3. Open and edit the config file `K.sh` in your favorite text editor:
```
 $ vim K.sh
```

To upgrade anytime to the latest release just run `make reinstall`.

### Configuration After Manual Installation

See [etc/K.sh.dist](https://github.com/ctubio/Krypto-trading-bot/blob/master/etc/K.sh.dist) file or better your own copy of `K.sh` file located in the top level path.

It just contains a few variables with examples. The very end of the file contains the code that starts the bot.

Once your config file is ready, you can execute it to start the bot:
```
 $ ./K.sh
```

Alternatively use `make start` to run `K.sh` in the background using [screen](https://kb.iu.edu/d/acuy) (to see the output, attach the screen with `make screen` [or run all at once with `make start screen`]).

Feel free to run `make stop` or `make restart` anytime, and don't forget to [read the fucking manual](https://github.com/ctubio/Krypto-trading-bot/blob/master/doc/MANUAL.md).

Troubleshooting:

 * If there is no wallet data on a given exchange, double-check the currency symbols with `--list` argument.

 Optional:

 * See `./K.sh --help` to trade or `make help` to develop.

 * Use your own SSL certificate with `--ssl-crt` and `--ssl-key`, see [web ui](https://github.com/ctubio/Krypto-trading-bot#web-ui) section. Otherwise, the unsecure built-in certificate is a fully featured default openssl, that you may just need to authorise in your browser.

### Upgrade to the latest commit

If you upgrade while having any instance running in the background, you will need to manually restart it using `make restart` or `make restartall` to start using the latest version.

#### Upgrade under Manual ZIP Installation:

Please run `make reinstall` to download the upgraded source and executable files.

#### Upgrade under Manual GIT Installation:

Feel free anytime to check if there are new upgrades with `make diff`.

Once you decide that is time to upgrade, execute `make upgrade` (or directly `make reinstall` to skip the validation of new commits).

If you only use `git` to pull the latest source files from the remote branch, you will still need to upgrade or recompile your executable files.

To not upgrade but instead recompile your own modified source files, use `make lib K` or just `make` (see [Build notes](#build-notes)).

### Multiple instances party time

Please note, an "instance" is in fact a `*.sh` config file; using a single machine with a single installation, you can run as many instances as `*.sh` files you have (limited by the available free RAM).

You can list the current running instances with `make list`.

If you haven't defined a config file, `make start`, `make screen`, `make stop` and `make restart` will use the default config file `K.sh`.

To run multiple instances using a collection of config files:

1. Create a new config file with `cp etc/K.sh.dist X.sh && chmod +x X.sh` (use `X.sh` or any name but keep `.sh` extension).

2. Edit the new config file `vim X.sh`

3. Run the new instance with `./X.sh` or to run in the background, use `K=X.sh make start`. To attach to the new instance's screen, use `K=X.sh make screen`. To stop the new instance, use `K=X.sh make stop` and to restart it, use `K=X.sh make restart`. The environment variable `K` specifies the filename of the config file that you want to use.

4. Open in the web browser the different pages of the ports of the different running instances, or display the UI of all instances together in a single page using the MATRYOSHKA link in the footer (that can be predefined using the optional argument `--matryoshka=URL`).

After multiple config files are setup, to control them all together instead of one by one, the commands `make startall`, `make stopall` and `make restartall` are also available, just remember that config files with a filename starting with underscore symbol "_" will be skipped.

### Application Usage

1. Open your web browser to connect to HTTPS port `3000` (or your configured port number) of the machine running K. If you're running K locally on Mac/Windows on Docker, replace "localhost" with the address returned by `boot2docker ip`.

2. Read up on how to use K and market making in the [manual](https://github.com/ctubio/Krypto-trading-bot/blob/master/doc/MANUAL.md).

3. Use the web UI to change the quoting parameters. Click the "BTC/USD" button to start making markets. Click it again to stop. When the button is green, the bot is actively placing orders.

### Web UI

Once `K` is up and running, visit HTTPS port `3000` (or your configured port number) to access the UI (i.e. [https://localhost:3000](https://localhost:3000)). There are inputs for quoting parameters, grids to display market orders, market trades, your trades, your order history, your positions, and a big button with the currency pair you are trading. When you're ready, click that button green to begin sending out quotes. The UI uses angularjs hydrated with websockets observed with reactivexjs.

If you want to generate your own certificate see [SSL for internal usage](https://www.akadia.com/services/ssh_test_certificate.html).

In case you really want to use plain HTTP, use `--without-ssl` argument.

### Databases

Each currency pair of each exchange will use a different sqlite database file with [WAL mode](https://www.sqlite.org/wal.html) enabled.

All database files are located at `/var/lib/K/db/K-*.db*`, outside the download folder to survive wild `rm -rf path/to/K` or reinstalls.

You can copy any group of `*.db*` files to another machine when migrating or as a backup.

If a database does not exist, the application will create it on boot; otherwise, it will use the existing one.

To explore each database you can use https://github.com/sqlitebrowser/sqlitebrowser or a similar tool.

To set a different database filename or to set an [in-memory database](https://sqlite.org/inmemorydb.html), use `--database=FILE` argument (see `--help`).

Even if using an in-memory database, the quoting parameters are always loaded from and saved into the disk file database.

### Charts

The metrics are not saved anywhere, it is just UI data collected with a visibility retention of `n` hours (where `n` is the value of `profit` quoting parameter), to display over time:

 * Market Fair Value with High and Low Prices
 * Trades Complete
 * Target Position for BTC currency (TBP)
 * Target Position for Fiat currency
 * STDEV and EWMA values for Quote Protection and APR
 * Amount available in wallet for buy
 * Amount held in open trades for buy
 * Amount available in wallet for sell
 * Amount held in open trades for sell
 * Total amount available and held at both sides in BTC currency
 * Total amount available and held at both sides in Fiat currency

### Cloud Hosting

If you ask me, [<img height="20px" src="https://user-images.githubusercontent.com/1634027/29756933-3e64c62e-8ba8-11e7-916a-3b0ae1481a52.png">](https://www.dreamhost.com/r.cgi?475987/cloud/) is a very nice web hosting company (awesome support team, awesome servers). Feel free to use this referral link to get a discount subtracted from my referral earnings (i'm a user since 2008).

### Build notes

Make sure your build machine has [node](https://nodejs.org/en/download/package-manager/) installed, also ensure `make lib` provides all dependencies without errors.

To rebuild the application with your modifications, see `make help` and choose a target (just `make` may be what you are looking for).

Test units are executed before the application exits, only if the application was compiled with `KUNITS=1 make`.

Otherwise, just `make` without the environment var `KUNITS` produces an application that simply exits on exit.

A quick test runner therefore is `./K.sh --version` or the alias `make test` or all at once with `KUNITS=1 make K test`.

To pipe the output to stdout, execute the application in the foreground with `./K.sh --naked`.

To ignore the output, execute the application in the background with `screen -dmS K K.sh` or with the alias `make start` or simply `./K.sh`.

For more information consider to follow the *white rabbit*, but its dangerous to go alone, take this:

c sandbox: [wandbox.org](https://wandbox.org)

js sandbox: [jsfiddle.net](https://jsfiddle.net)

ws sandbox: [websocket.org](https://www.websocket.org/echo.html)

<details><summary><a id="unreleased-changelog"><b>Release v0.6.x Changelog</b></a></summary>

Added Hello World bot and Scaling bot.

Added Binance, Kraken, KuCoin, Gate.io and BitMEX API.

</details>

<details><summary><b>Release v0.5.x Changelog</b></summary>

Updated exchange integrations as simple libcurl wrappers.

</details>

<details><summary><b>Release v0.4.x Changelog</b></summary>

Added main KryptoNinja class derived from all other classes and ready to be extended.

Added C++ OOP everywhere.

Added test units.

Added --interface=IP argument to bind outgoing traffic to a specific network interface.

Added Ethfinex ~~and FCoin~~ API.

Added build-in document root to stop reading files from disk.

Added build chain for win32.

~~Updated OKEx websocket to binary data.~~

Added build chain for OSX v10.13.
</details>

<details><summary><b>Release v0.3.x Changelog</b></summary>

Updated HitBTC API v2.

Added ZIP installation steps for non-git-lovers.

Added HamelinRat quoting mode and Trend safety thanks to b-seite and serzhiio contributions.

Added command-line arguments.

Updated quoting engine and gateways without nodejs.

Added Makefile to replace npm scripts.

~~Added PNG files as configuration files.~~

Added built-in C++ WWW Server to replace expressjs and socketio.

Added built-in SQLite C++ interface to replace external mongodb server.

Added Poloniex API.
</details>

<details><summary><b>Release v0.2.x Changelog</b></summary>

Updated application name to K because of Kira.

Added nodejs7, typescript2, angular4 and reactivexjs.

Added cleanup of bandwidth, source code, dependencies and installation steps.

Added many quoting parameters thanks to Camille92 genius suggestions.

Added support for multiple instances/config files with nested matryoshka UI.

Added npm scripts, david-dm, travis-ci, coveralls and codacy.

Added historical charts to replace grafana.

Added C++ math functions.

Updated OKCoin API (since https://www.okcoin.com/t-354.html).

Updated Bitfinex API v2.

Added Coinbase FIX API.

~~Added Korbit API.~~

Added new quoting styles PingPong, Boomerang, AK-47.

Added cleanup of database records, memory usage and log recording.

Added audio notices, realtime wallet display, and grafana integration.

Added https, dark theme and new UI elements.

Added a bit of love to Kira.
</details>

<details><summary><b>Release v0.1.0 Changelog</b></summary>

see the upstream project [michaelgrosner/tribeca](https://github.com/michaelgrosner/tribeca).
</details>

### Unlock

The bot is unlocked for collaborators and contributors (feel free to make acceptable Pull Requests for already opened issues or for anything you consider useful, and let me know the BTC Payment Address for the bot that you wish to unlock in the description of the PR, and I will credit it for you).

While locked, the orderbook will be in realtime 121 seconds, and later it will be updated only once every 121 seconds.

Anonymous users can also unlock any API Key by paying 0.01210000 BTC to the address displayed on exit.

Once unlocked you may use different bots or currency pairs or reinstall on a different machine with the same unlocked API Key. However, if you want to use more than one exchange, you will need to pay again to unlock the API Key for each exchange.

Otherwise if you choose to not support further development by ctubio, just keep running some old commit and do not upgrade (any commit prior to v0.3.0 was completely unlocked).

Please don't open issues asking how much % less the bot generates with `--free-version`; it is relative to your trading strategy, the market conditions, and the bot's performance.

### Donations

nope, this project doesn't have maintenance costs. but you can donate to your favorite developer today! (or tomorrow!)

or see the upstream project [michaelgrosner/tribeca](https://github.com/michaelgrosner/tribeca).

or donate your time with programming or financial suggestions in the IRC channel [#tradingBot](https://kiwiirc.com/client/irc.freenode.net:6697/?theme=cli#tradingBot) at irc.freenode.net on port 6697 (SSL), or 6667 (plain); or feel free to make any question, but questions technically are not donations.

### General Discussion

[IRC](https://kiwiirc.com/client/irc.freenode.net:6697/?theme=cli#tradingBot) is awesome!

but if you dislike it, consider to create a [new discussion](https://github.com/ctubio/Krypto-trading-bot/discussions) permanently readable by everybody.

