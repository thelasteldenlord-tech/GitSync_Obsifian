Yes, the open-source Mesa Turnip drivers for the Adreno 800 series have officially caught up. Released in early 2026, these drivers brought custom Vulkan support to both the Adreno 830 (Galaxy S25 Ultra) and the Adreno 840 (Snapdragon 8 Elite Gen 5). [1, 2] 
Before this breakthrough, the older Snapdragon 8 Gen 3 was actually preferred because the stock Qualcomm drivers on the 8 Elite family suffered from massive texture flickering, broken assets, and frequent crashes. Today, the Turnip drivers allow the raw power of these chips to be utilized, providing stable visuals, drastically fewer stutters, and high peak frame rates across AAA titles. [1, 2, 3] 
------------------------------
## Turnip Driver Maturity & Compatibility

* 
* The Current State: Visual bugs are largely fixed. Popular PC layers like GameHub Light and Winlator can run resource-heavy titles smoothly. [3, 4, 5] 
* Brute-Force Performance: The 8 Elite architecture is powerful enough to brute-force its way through unoptimized translation layers, delivering consistent performance. [5] 
* Quirks to Watch: Some modern titles (e.g., Mortal Kombat 1) may still exhibit minor texture glitching or hitching depending on the specific wrapper or driver revision (e.g., Mr. Purple Turnip vs Gen 8 v32). [6] 
* 

------------------------------
## Side-by-Side Performance Comparison
When comparing the Samsung Galaxy S25 Ultra (Snapdragon 8 Elite) to a flagship running the Snapdragon 8 Elite Gen 5, the generational shift is quite pronounced. The standard 8 Elite features two 4.32GHz Prime cores and six 3.53GHz performance cores. The 8 Elite Gen 5 ups the ante with two Oryon Gen 3 Prime cores pushed all the way to 4.61GHz and six performance cores at 3.63GHz. [7, 8, 9, 10] 
## 📊 Benchmark & AAA Gaming Performance Data

| Metric / Title | Galaxy S25 Ultra (Snapdragon 8 Elite) | Snapdragon 8 Elite Gen 5 Flagship | Performance Takeaway |
|---|---|---|---|
| Geekbench 6 (Single-Core) | ~3,100 points | ~3,800 points | +16% to 20% CPU uplift; significantly accelerates heavy x86 CPU instructions. |
| Geekbench 6 (Multi-Core) | ~9,300 points | ~12,400 points | +17% to 18% multi-core jump, preventing CPU bottlenecks in open-world titles. |
| 3DMark WildLife Stress Test | Base Score Loop | +16% (Peak) / +19% (Sustained) | The Adreno 840 architecture sustains higher graphics loops longer than the S25 Ultra. |
| Sekiro: Shadows Die Twice[](https://www.google.com/search?q=sekiro:+shadows+die+twice&kgmid=/g/11f69_k2sr) | 35–45 FPS (720p/Medium) | 55–60 FPS (720p/Medium/High) | The Gen 5 holds a locked, near-flawless 60 FPS frame rate with Turnip drivers. |
| GTA V[](https://www.google.com/search?q=gta+v&kgmid=/m/0hgnzjh) | 45–55 FPS (Normal settings) | 60+ FPS (Sustained) | The Gen 5 easily hits the 60 FPS engine cap with fewer frame drops during heavy physics sequences. |
| Cyberpunk 2077 / Witcher 3[](https://www.google.com/search?q=witcher+3&kgmid=/m/0qsc46_) | 25–35 FPS (Low/720p, highly volatile) | 40–50 FPS (Low/720p, more stable) | Gen 5 benefits heavily from the expanded 18MB high-performance graphics cache to combat memory throttling. |

------------------------------
## Crucial Hardware Factors to Keep in Mind

* 
* The Cooling Tax: Both devices run incredibly hot under Windows emulation. While the S25 Ultra can comfortably handle native Android games, running [Sekiro](https://www.google.com/search?q=sekiro&kgmid=/g/11f69_k2sr) or [GTA V](https://www.google.com/search?q=gta+v&kgmid=/m/0hgnzjh) pushes internal temperatures toward 80°C. To prevent hard thermal throttling down to 20 FPS on either phone, an active magnetic cooler (like a 25W Flydigi or Black Shark cooler) is mandatory. [3, 11] 
* Samsung's Aggressive GOS: The S25 Ultra is bound by Samsung's Game Optimizing Service (GOS). Even when disabled, it throttles faster than gaming-centric phones. The Gen 5 chip handles thermal efficiency better, meaning it requires less raw energy to hit the same frame targets as the S25 Ultra. [12] 
* 

Are you trying to figure out which specific Turnip driver revision to use on your S25 Ultra, or are you deciding which device to main as your primary pocket PC?

[1] [https://www.youtube.com](https://www.youtube.com/watch?v=DR8claNJtp8)
[2] [https://www.androidauthority.com](https://www.androidauthority.com/snapdragon-8-elite-8-elite-gen-5-devices-emulation-driver-3617718/)
[3] [https://www.youtube.com](https://www.youtube.com/watch?v=DR8claNJtp8)
[4] [https://www.youtube.com](https://www.youtube.com/watch?v=AOo9fZUvQOQ&t=360)
[5] [https://www.reddit.com](https://www.reddit.com/r/EmulationOnAndroid/comments/1n1jsiq/turnip_drivers_for_the_8_elite/)
[6] [https://www.reddit.com](https://www.reddit.com/r/EmulationOnAndroid/comments/1ugg7dw/what_is_the_best_turnip_driver_for_the_snapdragon/)
[7] [https://www.youtube.com](https://www.youtube.com/watch?v=YbDbouwiesY)
[8] [https://tech.yahoo.com](https://tech.yahoo.com/phones/articles/benchmarked-galaxy-s25-see-faster-144510240.html)
[9] [https://www.facebook.com](https://www.facebook.com/fb-answers/snapdragon-8-elite-gen-5-v-benchmarks/)
[10] [https://wccftech.com](https://wccftech.com/snapdragon-8-elite-gen-5-cpu-gpu-speeds-listed-by-tipster-with-new-antutu-score/)
[11] [https://www.youtube.com](https://www.youtube.com/watch?v=Oy90a8IR5JE)
[12] [https://www.reddit.com](https://www.reddit.com/r/Android/comments/1npnktv/snapdragon_8_elite_gen_5_the_worlds_fastest/)
