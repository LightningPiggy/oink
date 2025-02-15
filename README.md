# ZapNotify

A webapp (also installable as a Progressive Web App) that activates various notifications (sound, popup,...) when donations ("zaps") come in.

Live demo: https://oink.LightningPiggy.com/

Part of https://LightningPiggy.com/

# How to install and configure

1) Clone this project into a local folder on your PC or place the files into a webhosting service.

Tip: if you fork it in GitHub, and call the fork "\<yourusername\>.github.io" (without the "quotes") then
it will be publicly hosted by GitHub on https://yourusername.github.io (where yourusername is your username).

Read more about this, including custom domains, at https://pages.github.com/

2) Create a wallet on the LightningPiggy LNBits demo server: https://demo.lnpiggy.com

3) Copy-paste the Wallet's "Invoice/Read Key" from LNBits into this project's index.html file, in the apiUrl, on the first line below <script>.

For example, if your LNBits Wallet's Invoice/Read Key is 1c1077016ce746b6beae47c5890a8422
then in index.html, you should have:

```
const apiUrl = "wss://demo.lnpiggy.com/api/v1/ws/1c1077016ce746b6beae47c5890a8422";
```
4) Create a LNURLp(ay) link (= reusable payment string) in LNBits for the newly created wallet.

Enable the LNURLp extension in LNBits, click "NEW PAY LINK" and use settings such as:
- Wallet: choose the newly created lnbits wallet
- Item description: "Donation to LightningPiggy.com" (users will see this in their wallet when they zap)
- Lightning Address: oink (or whatever you like)
- Min: 1000 (default value that wallet will show)
- Max: 100000000 (is this too low?)
- Currency: satoshis
- Comment maximum characters: 255
- Webhook URL: not needed
- Success message (optional): Oink! Thank you! Oink, oink!
- Nostr: Enable nostr zaps

5) Copy-paste the lightning:LNURL link from LNBits into this project's index.html file.
Do the same for the lightning address (if you created one as part of the LNURLp setup).

For example, if your LNURLp link is lightning:LNURL1DP68GURN8GHJ7ER9D4HJUMRWWP5KWEME9E3K7MF0D3H82UNVWQHNVKN8FFE85WY0TEP
and your lightning address is oink@demo.lnpiggy.com then you should have in index.html something like:

```
<a href="lightning:LNURL1DP68GURN8GHJ7ER9D4HJUMRWWP5KWEME9E3K7MF0D3H82UNVWQHNVKN8FFE85WY0TEP" class="text-secondary"><img class="QR" src="QR.png"/></a>
<a href="lightning:oink@demo.lnpiggy.com" class="text-secondary"><h2>oink@demo.lnpiggy.com</h2></a>

6) Also replace this project's QR.png file with the QR code of the LNURL pay link. You can just right-click the QR code in LNBits and click "Save image as..."
```

# How to use

If the files are hosted somewhere (such as https://yourusername.github.io/) then open that website.
Or if you have them locally on your PC, open the index.html file in a webbrowser.

Click the "Enable audio and visual notifications" button to allow the browser to play audio (blocked if the user hasn't interacted with the page) and to connect the websocket and wait for incoming payments.

Note that you can also install the applications as a Progressive Web App.
Do this, in Chrome for example, by clicking the menu in the top right (three dots) and choosing "Install LightningPiggy Oink..."

# How it works

The index.html file opens a websocket to LNBits using Javascript.

LNBits sends a notification over that websocket when a payment comes in.

The index.html parses the incoming payment data (amount, comment), plays an MP3 and shows a message and the comment to the user for 10 seconds.
