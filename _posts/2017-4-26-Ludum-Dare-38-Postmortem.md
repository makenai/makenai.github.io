---
layout: post
title: LD38 - "NO STEP ON HYOOMINS" Postmortem
---

This was my first Ludum Dare. I've been aware of the event for a long time and had planned to participate before, but this is the first time I followed through. I've been at kind of a personal and creative lull so far this year, so I was looking for something to awaken my passions and thought this might be it.

If you're not familiar with Ludum Dare it's a weekend game jam and competition that happens every 4 months on the internet. You are tasked with creating a game in either 48 (hard mode) or 72 hours that fits in (optionally) with a community selected theme. You can read the [rules](http://ludumdare.com/compo/rules/) for more details.

This time the theme was 'A Small World'. I had a few general ideas including creating a game that took place on the Small World Disneyland ride, but eventually settled on the idea of becoming a giant that tries not to step on people in a small world. I thought that it would be simple enough to do in a couple of days, kinda funny, and that it could have an interesting control mechanic with draggable feet.

Here is a link to the game:

[<img src="https://img.itch.zone/aW1hZ2UvMTM4MjczLzYzMjQ1My5wbmc=/315x250%23c/iHvGKb.png" alt="screenshot"><br /> No Step On Hyoomins @ Itch.io](https://makenai.itch.io/no-step-on-hyoomins)

I also recorded a time lapse video of the creation process. Doing that or something like a live stream is pretty common for these game jams:

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZYQxab8NXqo" frameborder="0" allowfullscreen></iframe>

Another thing that is pretty common is writing  post mortem that talks about what went right and what went wrong, and that's what you're reading now! One of the great things about the videos and post mortems is that they're educational to newcomers. I looked over a few of them myself before signing up for this now, and now I'm happy to add my experiences to the available pool.

# What Went Right:
------------------

## 1. Using PhaserJS

I am a web developer who uses JavaScript every day for work stuff, so I thought I'd be better using a language I know well. Last year I saw a fun [talk](https://www.youtube.com/watch?v=2oKSSnEgBDw) by [Rachel White](https://twitter.com/ohhoe) about PhaserJS and really wanted to use it for something.

Phaser made a lot of things a breeze. The built in support for various file formats for things like sprite sheets, bitmapped fonts, tilemaps and more made it super easy to cobble things together quickly. The community support and docs were top notch. The drag and drop and interactions work on both mobile and desktop flawlessly. The scale manager and game states are amazing.

Maybe some of these things are pretty standard in modern game frameworks, but I really appreciate them! I've only written games years and years ago (Basic, Pascal, C) when things seemed much harder and any frameworks that existed were much more limited in scope. Even if these features are standard, I think they are executed very well and in an easy to understand manner in Phaser.

## 2. Using phaser-node-kit

One of the most painful aspects of JavaScript web development is setting up toolchains. You can develop a Phaser app just using a text editor and phaser.min.js, but you'll have to include each file in your HTML individually and worry about things like namespacing and order of dependencies if you're writing client side JS code.

We tend to use collections of tools to get rid of some of these limitations by using things webpack that allow us to require files and modules and pack them into a couple of optimized script files, but they are a pain to set up. I found a package on NPM called [phaser-node-kit](https://www.npmjs.com/package/phaser-node-kit) that did a great job setting up a boilerplate project and coupled it with browserify and a local web server to make local development a breeze with no dependency issues. Note: a local web server is required for running phaser games because of cross origin security policies.

## 3. Cramming before the jam

I felt a little unprepared going into the jam since I haven't done much game development, so I spent a few evenings of the week leading up to the jam studying various topics.

I started by reading [Game Jam Survival Guide](https://www.packtpub.com/game-development/game-jam-survival-guide), which I got a free copy of years ago as part of some promotion. It was still sitting in my Packt account waiting for me. This gave me a few good pointers and a better idea of what to expect. A few things I took to heart:

- Reducing scope to fit available time and keeping things simple
- Thinking out of the box with the theme / using a thesaurus etc. for various interpretations of the words
- Not worrying about elegant code and using hacks to get things working
- Optimizing for fun in the first 15 seconds of game play since that's how much most people spend
- Funny or "Joke" games tend to do well

I also went through the [HTML5 Game Development with Phaser](https://www.lynda.com/Phaser-tutorials/HTML5-Game-Development-Phaser/163641-2.html) tutorial on Lynda to get up to speed on the framework. It was pretty helpful beyond the documentation to see how a full game goes together. I didn't write much code before the actual jam, but after watching this tutorial I had a mental palette what was available and how to accomplish certain things.

I also spent some time downloading and familiarizing myself with various asset creation tools. I looked at [Tiled](http://www.mapeditor.org/), [Texture Packer](https://www.codeandweb.com/texturepacker), [ASEprite](https://www.aseprite.org/), [Pyxel](http://pyxeledit.com/) and [Spriter](https://brashmonkey.com/). I mostly watched video tutorials and made sure I understood the basics of how each tool worked just in case I needed them for the jam. I ended up using Tiled, Texture Packer, and ASESprite to set up a map, create a sprite sheet, and create animations.

I was really inspired by the tutorials for Spriter and totally into the way the animation tools work! I didn't get to use it this time, but I'll be looking for an excuse. I used to do a little bit of Flash development, so the process was pretty familiar to me and it looks like it makes animating a lot more fun by moving limbs around rather than redrawing entire sprites as one would with ASEprite.

## 4. Not working 24/7 on this

In total I spent about 12 hours working on this game out of the 72 or so available for the jam. I didn't stay up too late at night, though I had a small cache of sugar free red bull just in case it came to that. I got off to a good start on Friday night. On Saturday I had pretty much the whole day free with zero distractions, but I wasn't really feeling up to the task in the morning. I visited my parents for a bit instead. When I got back home, I had another fairly productive few hours in the evening. On Sunday, I went for a long hike with the family, then worked on the game for an hour or so before a weekly dinner with have with our whole family (my family, my sister's and my parents). After dinner when we got home and put the kids to bed, I was able to get most of the basic game mechanics completed.

I took part of my normal work day on Monday to put some finishing touches on the game including titles, sound, music and packaging.

When it was done, I felt pretty good about what I had accomplished. I wasn't feeling burned out or exhausted and I didn't feel guilty about shutting out my family during the family because I hadn't (too much). I could have probably come up with a much more impressive game if I had put more time into it, but this was a good compromise for me.

## 5. Hacky collision fixing + hacky things in general

I had a lot of trouble with collision detection since the two shoes I used were pretty oddly shaped and had some transparent areas that detected as false hits. As far as I know, the basic arcade physics mode in Phaser only  supports a single collider per sprite that is either a rectangle or a circle. Neither of those worked too well for my long and oddly curved shoe sprites. I was hoping to find a pixel perfect collider or a good solution to the problem but I couldn't find one.

There is a P2 physics mode that uses more advanced polygon colliders, but I didn't want to sink more time into learning it and possibly breaking something else after already sinking quite a bit of time into research and trying out things that didn't work. I ended up writing a really dirty secondary collision filter to reject collisions based on a bunch of x,y coordinates and a switch statement. Probably spent 2 hours on this problem alone, but the quick hacky solution took about 15 minutes more and solved the problem to "just about good enough" level.

There were other places where I saved some time by using kind of sloppy coding practices such as attaching arbitrary properties to sprites to keep track of things - things that I wouldn't let myself do for normal production code but I allowed myself to do because game jam! It kinda felt good in the way that getting away with something harmless but a little naughty feels good. It was a little cathartic too.

## 6. Passions Awakened

Probably the biggest thing that went right is that now I'm excited about making another game in the future and learning new game systems like Unity. This is easily the biggest win for me!


# What Went Wrong:
------------------

## 1. Wanting to make my own assets

One of the rules of the 48 hour compo that is not part of the 72 hour game jam is that you have to create all your own assets instead of just using freely available ones. I had originally hoped I'd be able to create all my own assets, but in the end it would have been just too time consuming. I think the first few I picked up, I was hoping to use as placeholders and then replace eventually but there wasn't time to do that! Maybe in an even simpler future game, or if I get more proficient at graphics work.

## 2. Not including buildings

I originally wanted to create buildings hazards and things you had to avoid stomping on, but I wasn't able to get that done. I was thinking about using a tileset with buildings, but I couldn't find a set I really liked. I would also have had to implement collision detection with specific tiles and add destructive terrain. All this would have taken a lot more time.

In the end, I found a kind of simple flat [2D tile set](https://www.youtube.com/watch?v=EDztZsx1k6w) from [James Arndt](https://www.youtube.com/channel/UC8wwKKr-GpntrUnFpN15kVw) that featured some streets and grass. I did a little bit of image processing and rotation to get them into a Tiled compatible format. Since they were so simple, it was pretty easy to spend a few minutes laying out a very, very basic map.

I thought I could add some buildings later on, but didn't have the chance. I decided to just leave it as is and concentrate on the mechanic of avoiding tiny humans. However, since there were no other obstacles, I had to greatly inflate the number of random people wandering around on the map.

I kind of wish I had spent a little more time laying out the map and making it look more like a city. I also wish that I had added a few more buildings and things so it wasn't just an empty lot with a bunch of people wandering aimlessly!

## 3. Kind of a gross feeling game

I originally wanted to make this kind of a friendly and funny game. The original working title was 'Gentle Giant' and the point is to NOT step on people. My original mental pitch described it as sort of a reverse 'Rampage' where you try not to destroy stuff.

I think it didn't dawn on me that I needed to have something happen visually when you stepped on people in the early stages. I ended using the blood pool because it was a strong visual indicator that something bad had happened. Later, when I was debugging collision detection, I wanted to make sure the blood pools were spawning in the same places as where the people sprites were getting stepped on, I 'froze' the people sprites in place instead of removing them from the game. I kinda liked the way that looked, so I decided to leave 'bodies' in. Finally I wanted a font to match the game a bit and I ended up going with a drippy bitmap font.

When I got to the end of everything, I took a step back and looked at it and though "this doesn't feel good to me at all". I think there's certainly a place for kind of gorey stuff in videos games, but it's not necessarily the kind of game I wanted to make. Hopefully some people find it a little funny, but I'm also sorry if you tried it and it was an unpleasant experience for you.

My next game will probably have more puppies and kittens.