---
title: "Dev ports Half-Life to the PS1, asks Valve if it's cool with that, and says he'll \"make it public\" if he doesn't hear back in a month"
source: "https://www.gamesradar.com/games/fps/dev-ports-half-life-to-the-ps1-asks-valve-if-its-cool-with-that-and-says-hell-make-it-public-if-he-doesnt-hear-back-in-a-month/"
author:
  - "[[Austin Wood]]"
published: 2026-07-31
created: 2026-08-05
description: "Not an emulator and not a demake"
tags:
  - "clippings"
---
![Gordon Freeman in Half-Life on orange background](https://cdn.mos.cms.futurecdn.net/y5Zg6AzhaMqQtPs5SWQri8-1920-80.jpg.webp)

(Image credit: Valve)

People are really out here porting Half-Life to the PlayStation 1.

Manny, of [Bonnie Studios](https://www.youtube.com/@bonnie-studios-dev), is a self-described "software engineer, guitarist, and game developer from Sicily." His debut [YouTube](https://www.gamesradar.com/tag/youtube/) video promises "Half-Life on a Real PlayStation 1," and 14 minutes of glorious 1998 technology revisited with 2026 technology bears that promise out.

"Not an emulator and not a demake: a renderer and game runtime written from scratch in Rust," Manny stresses.

Latest Videos FromGamesRadar+

Manny is more broadly known for [PSoXide](http://youtube.com/redirect?event=video_description&redir_token=QUM4Zm9rUUgxT25BbERaVDJGTzl1dE5NRDYxNnxBR3JiS2FrOGdyN3pTUy1LN3NPVTF2ZnZFeFZUel9xbWpFcmJ3U2FTS2VrN3VEVnQ5cGxoMUFSZ3pwZ2hHRFEyMmFSVXZQbDA1YnNLRnU4VjRjU1MwNmJuM1RvcFczck5vVVhv&q=https%3A%2F%2Fgithub.com%2FEBonura%2FPSoXide&v=aEaa9CeCsbQ), a PS1 development tech stack that, per his [Itch.io](https://bonnie-studios.itch.io/) page, covers an "emulator + Rust SDK + game engine + editor + asset pipeline." In this case, Half-Life was written fully for the Rust coding language without reliance on a traditional emulator, and is running on a proper PS1 console – in this case, "direct capture" off an SCPH-9002 model PS1.

"This is the full Hazard Course, all seven maps, start to finish in one sitting with no cuts," Manny explains in the video description. The Hazard Course is basically the tutorial prologue for Half-Life – a good sandbox for a demonstration like this.

"The deaths, the retries, the moment I get stuck inside a wall and die, and the audio glitches are all still in it," Manny asserts. "It averages around 17fps, holding 20 most of the time and dropping to 10-16 in the widest areas. The capture chain adds about 100ms between the pad and the picture, so it plays tighter on the console than it looks here."

As a quick refresher, the PS1 was released in North America by [Sony](https://www.gamesradar.com/tag/sony/) in 1995, [Valve](https://www.gamesradar.com/tag/valve/) dropped Half-Life in 1998, and the significantly more powerful PS2 arrived in 2000. Lauded for its advanced tech and physics, Half-Life launched on PC and only came to the PS2 in 2001.

Getting the game running *at all* on a system that predates it by several years is pretty impressive work, even if artifact-like graphical distortions do make it look like protagonist Gordon Freeman pounded back a few benadryl cocktails garnished with melatonin gummies before work.

I can't help but wonder if the AI-generated code that evidently went into the project played a part in that oddness, too, for all Manny's [assurances](https://www.reddit.com/r/HalfLife/comments/1v7ardl/comment/ozy36qj/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) that his "pre-AI coding background" and "core decision" shaped the programming. AI use in ports like this has [become a battleground](https://www.gamesradar.com/games/donkey-kong/donkey-kong-64-pc-recompilation-rejects-ai-vibe-coding-as-devs-try-to-build-a-port-of-actually-good-quality-before-our-competitor-releases-their-poorly-made-one/), with some teams targeting specific games just to outdo what they call vibe-coded slop. And GamesRadar+ has extensively covered [why game developers in general don't want to use generative AI](https://www.gamesradar.com/games/why-so-many-game-developers-dont-want-to-use-generative-ai/) in any capacity.

![Gordon Freeman](https://cdn.mos.cms.futurecdn.net/6KMkD6TBUDtbuAUSbQ9tAc-1200-80.jpg.webp)

(Image credit: Valve)

Manny lays out just "some" of the workarounds necessary to fit 10 pounds of game into a 5-pound console: "BSP traversal doubling as painter's order for the ordering table, PVS culling, 16 colour CLUTs at 4 bits per pixel, LZ4 map chunks streamed into a static buffer, animation frames pre-posed at cook time because there is no FPU and no heap, SPU ADPCM audio and 27 Red Book CD tracks on the disc."

Which is all to say: squeezing blood from stone.

This being a fan effort, Manny says he's reached out to Valve "asking them to greenlight the project" before releasing the source code. "For legal reasons there will never be a downloadable disc image or a ready-to-play build," he adds. But if Valve miraculously gives him the thumbs up, or if he has "not heard back in a month or so," he says "I will take that as no objection and make it public."

Manny is doing much better than the company that promised and sold a Portal-inspired Steam Machine Companion Cube case ["without ever asking Valve" for permission.](https://www.gamesradar.com/hardware/desktop-pc/selling-a-portal-inspired-steam-machine-companion-cube-case-without-ever-asking-valve-was-pretty-stupid-admits-company-now-issuing-refunds/)

"Once released you will need your own lawfully obtained Steam copy of Half-Life: the converter reads it on your own machine and builds the disc from there," Manny adds. That, and you'll need a PS1.

On Twitter, Manny reveals that his next project hopes to get "Minecraft-style worlds running natively on PlayStation 1 hardware." That's full "chunk streaming, day/night, mobs and caves on a 33MHz CPU."

Earlier this month, [a designer at Valve recreated Half-Life 2's Ravenholm](https://www.gamesradar.com/games/fps/a-current-valve-designer-recreated-half-life-2s-ravenholm-in-the-source-2-engine-and-says-he-was-blown-away-at-how-powerful-these-tools-are/) in the company's new Source 2 engine, saying he was "blown away at powerful these tools are."

[*The "final game" from Half-Life 2 and Dishonored's late art director has been revealed: "The world's first Soulslike FPS," an apocalyptic Western at "the end of America."*](https://www.gamesradar.com/games/fps/the-final-game-from-half-life-2-and-dishonoreds-late-art-director-has-been-revealed-the-worlds-first-soulslike-fps-an-apocalyptic-western-at-the-end-of-america/)

Do you prefer buying physical or digital games?

Physical

Digital

Depends on the game

Thanks for voting!

Join the community

Join the GamesRadar+ Family! The best way to keep in touch and to be informed of our latest quizzes and competitions, as well as news and offers.

Already have an account? Log in

My Details

Update your details below...

Keep in the Know

Would you like to be kept informed about new quizzes and offers from Future and its partners?

Validate Your Mobile No.

We have sent a code to. Please enter it below to verify your account.

Update Your Mobile No.

You may enter a new mobile number below. You will be sent a verification code to the phone number you provide.

embed-poll.hint\_heading

embed-poll.hint\_subheading

Validate Your Email Address

We have sent a code to. Please enter it below to verify your account.

Update Your Email Address

You may enter a new email address below. You will be sent a verification code to the address you provide.

Create a Username

This will be publicly viewable so make it something you like!

Reset your password

Enter your email address below. If it is registered with us, we will email you a code that will allow you to reset your password.

Check your inbox

If your email address was found in our system, you should receive an email in the next few minutes containing a code. Enter that code below to reset your password.

Set new password

Please enter your new password below.

Leaderboard

| Rank | Player | Score | Time |
| --- | --- | --- | --- |

LATEST ARTICLES

1. [
	![Kingdom Come: Deliverance 2 screenshot showing a group of medieval men sitting at a table with food, cheering together with wooden mugs of beer lifted high](https://cdn.mos.cms.futurecdn.net/XgWdkgRZT8hx3ydRet3Rrf-1280-80.jpg.webp)
	](https://www.gamesradar.com/games/action-rpg/kingdom-come-deliverance-2s-hans-actor-takes-his-role-so-seriously-that-hes-opening-a-real-medieval-inspired-bar-in-the-czech-capital-prague/ "Kingdom: Come Deliverance 2's Hans actor takes his role so seriously that he's opening a real \"medieval-inspired bar\" in the Czech capital, Prague")
	1
	[Kingdom: Come Deliverance 2's Hans actor takes his role so seriously that he's opening a real "medieval-inspired bar" in the Czech capital, Prague](https://www.gamesradar.com/games/action-rpg/kingdom-come-deliverance-2s-hans-actor-takes-his-role-so-seriously-that-hes-opening-a-real-medieval-inspired-bar-in-the-czech-capital-prague/)
2. 2
	[EA and games like The Sims, Dragon Age, and Battlefield are now officially owned by Saudi Arabia and private equity as $55 billion deal closes](https://www.gamesradar.com/games/ea-and-games-like-the-sims-dragon-age-and-battlefield-are-now-officially-owned-by-saudi-arabia-and-private-equity-as-usd55-billion-deal-closes/)
3. 3
	[Shang-Chi would have "two sequels already" if the industry hadn't gone to "s\*\*\*" when it was released, director says](https://www.gamesradar.com/entertainment/marvel-movies/shang-chi-would-have-two-sequels-already-if-the-industry-hadnt-gone-to-s-when-it-was-released-director-says/)
4. 4
	[The biggest Baldur's Gate 3 save scummers slammed quicksave over 1,400 times in one go, Larian says: "You doing okay there?"](https://www.gamesradar.com/games/baldur-s-gate/the-biggest-baldurs-gate-3-save-scummers-slammed-quicksave-over-1-400-times-in-one-go-larian-says-you-doing-okay-there/)
5. 5
	[Wonder Man co-creator says Kevin Feige didn't cancel season 2 of the acclaimed Marvel show: "I know he loves that show as much as I do"](https://www.gamesradar.com/entertainment/marvel-tv-shows/wonder-man-co-creator-says-kevin-feige-didnt-cancel-season-2-of-the-acclaimed-marvel-show-i-know-he-loves-that-show-as-much-as-i-do/)