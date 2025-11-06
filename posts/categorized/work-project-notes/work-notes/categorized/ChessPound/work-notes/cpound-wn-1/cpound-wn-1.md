---
title: 'cpound-1 work notes'
date: '2024-04-11'
---

I REALLY don't want to create a custom state system.


Okay, to make the green and red alerts than what we have to do is have it be really fast, which is a justification for having it be Linux desktop. 

We also want to make it WASM because that may make it faster for running the Chess evals. 


Start: 
Sun Sep 21 11:45:13 AM CDT 2025


What I want to do is... 


Really on the MoLStack side I would like a way to play like an audio file here.


And play it but from this nvim instance and not have to add a bunch of utils to the terminal to make it work.


What I realized why .NET is dope esp. Avalonia because it is really good at cross-platform apps and I'm a Linux user and the main drawback of Linux is compatabillity and things just not working out of the box. 

You know what they say, Linux is free if you don't value your time. 




It could be like, Sicillian vs. King's Indian or what have you. 

Start:
Tue Sep 23 05:42:01 AM CDT 2025





I want to get focused on the business logic viz. the part of the game I WANT. This part is practicing middle game positions. 


Start: Sat Sep 27 06:26:19 PM CDT 2025


I think today marks the day where we've reached the point of critical mass and vibe coding no longer works.



Start: Tue Sep 30 04:37:47 AM CDT 2025
Tryna get the COTA1 into COTA2



Start: Sat Oct  4 11:02:55 PM CDT 2025


I'm tryna get my Cursor IDE to detect .NET/C# errors. 

Okay so I fixed that.


Aside: 

I would like to just ctrl+alt+t write my GH Issue down and then take that buffer of the Vim instance. 

Start: 
Sun Oct  5 12:48:02 PM CDT 2025


So I have to make it like a custom implementaion for WASM because there isn't a stack which exists which can just talk to a WASM container without a JavaScript bridge. 


...

I would like to study how LiChess does their bots and how they run it.

I feel like the Legacy Chess Companies aren't using Server Side WASM.



...

Start: Wed Oct  8 07:37:03 PM CDT 2025

dotnet test --logger "console;verbosity=detailed" --filter "PlayStockfishAndMakePawnMove"



...

Start: Sun Oct 12 02:20:39 PM CDT 2025

This:
https://github.com/MonteLogic/COTA3/blob/bd34bd008a9baf43a5384f612331cd73ac6357a5/ChessOnTheAv3/Services/WebAssemblyStockfishService.cs#L210


We know CallWasmStockfish isn't getting the string param.


This is a useful file/page:
http://localhost:5236/stockfish-detection-test.html



Currently:

✅ Stockfish API
The global `Stockfish()` constructor was found.
This is the correct entry point for the engine.
❌ Stockfish Move Generation
Error during instantiation or communication.
Stockfish is not a constructor
✅ JavaScript Errors
No JavaScript errors were detected during the test run.
[3:55:22 PM] 🔍 Starting Corrected Stockfish Detection Test...
[3:55:23 PM] 🔍 Testing for Stockfish API availability...
[3:55:23 PM] 🔍 Testing Stockfish move generation via official API...
[3:55:23 PM] Attempting to create a new Stockfish() instance...
[3:55:23 PM] ❌ Error during move generation: Stockfish is not a constructor
[3:55:23 PM] 🔍 Checking for JavaScript errors...
[3:55:23 PM] 
📊 Test Summary: 2/3 tests passed
[3:55:23 PM] ⚠️ Some tests failed. Check console for errors.



Start: 
Sun Oct 19 09:26:14 AM CDT 2025


What I really want to do is.... 

I want to do it in Next.js but have it interop with a client side stockfish.wasm file. 


Or use Rust instead of Next.js 
But I have to make this work with dotnet and ASP.NET.


.... 


Okay, so I found out mannual placement of .wasm files isn't a thing and that the .wasm file is built with a paired .js file and these files should be built everytime so like dotnet build. 


...  

Okay, so dotnet is done for a good minute, so I am going to use Next.js + Rust to get it done and then go back to using Blazor UI.


So the plan is to do Rust + Next.js and write those .wasm files using Rust and understand on a deep level what's in those .wasm files. 



The dotnet stuff I feel like I got kind of close but I just feel like I'm going to have to use a different engine and know more about how .wasm files are instantiated. 






































