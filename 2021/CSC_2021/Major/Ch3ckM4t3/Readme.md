# Ch3ckM4t3

>Description: \
>You work as a counter-intelligence agent we intercepted this strange exchange between 2 enemy spies see if you can find any hidden message

We are given a video of a chess game. The game itself is fairly suspicious as neither player seems to be attempting to win. \
The file doesn't contain anything suspicious so some further research is required: \
Googling around for Steganography and Chess gives us an interesting tool that can encode data into \
a chess game and export it as a PGN. \
https://incoherency.co.uk/chess-steg/ \
I didn't find any quick wins on converting an mp4 into a PGN file so I had to replay the game manually on lichess: \
https://lichess.org/analysis#0 \
```
1. b3 Na6 2. Na3 c5 3. b4 h6 4. Bb2 Nc7 5. e3 Nb5 6. Bc3 Nf6 7. Bxb5 Qc7 8. h4 e5 9. Ke2 c4 10. Qe1 Ne4 11. Rh2 Rh7 12. Rh3 Qd6 13. Rc1 Nxd2 14. Bc6 h5 15. Rh1 Nb3 16. axb3 Rh6 17. f3 Qe7 18. Kf1 dxc6 19. Rd1 g6 20. Nb5 g5 21. Bb2 Qd6 22. Nc3 Bg4 23. Ke2 Bd7 24. Nd5 Rc8 25. Nf4 e4 26. Be5 Qc7 27. Bc3 Kd8 28. Rd6 Qa5 29. Qd2 Rh7 30. Qd5 Qa4 31. Bg7 Bxg7 32. Kd2 Qb5 33. g4 Rh6 34. Nd3 Kc7 35. Qe5 Rg8 36. Kc1 Be8 37. Qd4 b6 38. c3 Re6 39. hxg5 f6 40. Qc5 hxg4 41. Rd8 Bh5 42. Rc8+ Kd7 43. gxf6 Rge8 44. Rd8+ Kxd8 45. fxe4 Bxf6 46. Kb1 Rd6 47. Rh3 Rd7 48. e5 Qa4 49. Nf2 Rd3 50. bxa4 bxc5 51. Kc2 Rd7 52. Kc1 Rd2 53. bxc5 Rb2 54. Rh1 Bxe5 55. Ngh3 Rc2+ 56. Kxc2 Re6 57. e4 Bd4
```
Decoding with chess-steg:
```
flag{3b663edb9689ccb0c0eb87a00d71bb4321a3523069ff79ae0e17b0281ccbe3ea}
```
