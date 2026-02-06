Maclock from WonderBoy is a cute and surprisingly accurate-looking desk clock that looks like an original Macintosh. Its potential is wasted as just a clock, so a natural question is, can you swap its internals for a Raspberry Pi?

The answer, of course, is yes.

This repo covers the software steps to get the Mini vMac emulator working on a modern Raspberry Pi OS. Sadly the Mini vMac project has seen little development lately, and as of Feburary 2026 the binaries offered on its site (https://www.gryphel.com/c/minivmac) won't run on newer OS versions like Bookworm or Trixie. Thankfully, it's possible to compile it from source using the latest beta. Instructions on how to do that, plus links to some other resources you'll need to get the WonderMac working as a mini Mac, are covered here.

I didn't really write any groundbreaking code here, and while I'm not including the actual source files for Mini vMac, I marked this project as GPL v2 to match what Mini vMac is licensed as. If that project ever disappears, I may host a copy of the source files here for posterity, so this covers for that (hopefully unlikely) scenario.

I'm honestly not planning on keeping up with this project much, so don't expect updates. I'll try to include notes at points where doing your own homework is advised (looking up the URL for the latest Mini vMac source, etc). I also can't really offer much in terms of troubleshooting; I'm not a developer, just a hapless YouTuber who slapped some stuff together to make this thing work, so you're pretty much on your own. If you can make this process better/easier/faster/whatever, go for it!

Start with the prerequisites doc to get your Raspberry Pi set up, then proceed to the set-up-minivmac doc. The whats-next doc is useful to folks who don't have experience with Mac emulation.
