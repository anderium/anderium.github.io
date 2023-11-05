# Created sudokus

This is, for now, a short list without any introduction.  One day I'll get around to writing that as well, surely.

I meant to create a consistent naming scheme for my sudokus, so I attempted to find names of old games that fit the
intended solution path for the puzzles.  I didn't succeed, because the feeling each sudoku gives off doesn't fit with
the names I could think of.  Instead, all my sudokus are written in small caps if their title is a feeling, and ordinary
characters if they are part of the Domino Sums series.

## List

Sudokus in reverse order of creation.

1. **Domino Sums 102**.  [Full image](./images/domino-sums-102.png).
1. **Domino Sums 101**.  [Full image](./images/domino-sums-101.png).
1. **Domino Sums**.  [Full image](./images/domino-sums.png).
1. **Dancing snakes**.  [Full image](./images/dancing-snakes.png).
1. **Space invaders**.  [Full image](./images/space-invaders.png).
1. **Crosses and dots**.  [Full image](./images/crosses-and-dots.png).
1. **Snakes and ladders (0)**.  [Full image](./images/snakes-and-ladders-lvl0.png).
1. **Snakes and ladders**.  [Full image](./images/snakes-and-ladders.png).

## Solutions

Because I do not intend to give full solutions, you will have to calculate the SHA256 sum for the string of the rows
directly concatenated.  (E.g. for a 4 by 4 sudoku that might be `sha256(1234341241232341) == 6db89a...`.)  You can get
this easily from the command line with `echo -n solution | sha256sum` on Linux and `echo -n solution | shasum -a 256` on
MacOS.

If I made a mistake with entering the solution, please open a Github issue or message me so I can double check it and
update the hash here if necessary.

1. **Domino Sums 102**:  `eb4268d8aca8c7c190f6050dbeab6d1c77e99745cdb999a99fec51ec8d5a38e3`.
1. **Domino Sums 101**:  `ea9ff65fd14e7fa1edf34f0a64a188ea95cb1efd4a863dfd536ce1727adbd268`.
1. **Domino Sums**:  `774ffa1a088e660904d634bdf3d15ef1d15dc1c5ba2077a3fddf1e06ac397314`.
1. **Dancing snakes**:  `aa3f819d1424a82373d21abf41c3f5a010bbf79b2a51542a18c2885177b905e5`.
1. **Space invaders**:  `69e31af019a281b3e3b59e28199dce0fa67384c61c91a7aa80b2cc1a1595ff9a`.
1. **Crosses and dots**:  `9fd780d026889a0e0a510fff1f74495fd3c249c722d1664986b2f60bfe006277`.
1. **Snakes and ladders (0)**:  `62ece6b9c17bb2403e247ac4316ddca81b28ac701162cdd774cd7309de7f4653`.
1. **Snakes and ladders**:  `9e3f88814d8ae1219b9b30c2117f4189f8b36416374453ca4bf044fbd654bc92`.
