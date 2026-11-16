# Tap When

A party-game prototype. Each round names one thing to wait for: a carnivore, a landmark in France, an EGOT winner. Slides flash by, and the first hand on the big red button while the right one is showing wins the round.

- A new slide comes up every 2 seconds (1.3 or 3 from Settings), after a three, two, one.
- The right slide can be the very first, or take up to 30 seconds to turn up. It stays up no longer than the others.
- Hit it inside 0.8 seconds and the round is a quick draw, worth double.
- A wrong tap buzzes and names the slide you hit, and you sit out the rest of the round. Settings can make a wrong tap end the round instead.
- If the right slide goes by untapped, nobody scores.
- Ten rounds. Most points wins.

There are 61 reels on six shelves: animals, landmarks, art, space, flags, and names and numbers. Each game draws ten. Eight of them are size comparisons: bigger than Earth, a person, the Mona Lisa, Texas, a breadbox, a baseball or a million, and taller than the Statue of Liberty.

## Running it

`index.html` is the whole game and `img/` holds its slides. There is no build step and nothing to install; the only outside dependency is two Google Fonts. Open `index.html` in a browser, or serve the repo with GitHub Pages.

On an iPhone, "Add to Home Screen" runs it full-screen.

## Changing it

Everything below is in the one `<script>` block in `index.html`.

- **Reels** are the `REELS` array. A reel is one thing to wait for:

  ```js
  { id: 'bear', pool: 'animals', q: 'a bear', nn: 'Not a bear.',
    yes: [['polarbear', 'The largest bear there is.'], ['panda', 'Giant pandas are true bears.']],
    no:  [['koala', 'Not a bear. Koalas are marsupials.'], 'bison', 'gorilla', 'moose'] }
  ```

  `yes` are the slides that count and `no` the ones that don't. An entry is a slide id, or `[id, 'a line for the result slip']` when there is something worth saying. `yn` and `nn` are the lines used when an entry has none. `pool` is the shelf the reel sits on (`animals`, `landmarks`, `art`, `planets`, `flags`, `words`), and `x` marks reels too alike to both turn up in one game.
- **Word reels** (`words: true`) flash names or numbers on title slides and need no images. Their entries are the text itself.
- **Slides** are 900 × 600 WebP files, the 3:2 of a 35mm slide. To add one, put `name.webp` in `img/`, give it a display name in `NAMES`, and list `name` in a reel.
- **The rules as numbers** are the constants at the top of the script: rounds per game, the 30-second ceiling, the three paces, the quick-draw window, how long a wrong tap freezes the reel, and how many reels each game takes from each shelf (`MIX`).
- **Colours and fonts** are tokens in the `:root` block at the top of the stylesheet. The finish for each round is `ROUND_PAIRS` in the script.

Three reels depend on things that change, and were checked in November 2026. EGOT: 22 winners, Steven Spielberg the most recent. The men's World Cup: Spain won in 2026, its second title. The G7: the same seven members at the 2026 summit.

Settings are remembered per device. On a site that also hosts Perfect Timing, Tap When starts in the typeface chosen there.

## Picture credits

The pictures are openly licensed stand-ins for prototyping, not final art. They keep their own licences, listed here; nothing in this section covers the game's code. Every image has been cropped and resized to 900 × 600. Portrait and panoramic photos sit on a blurred copy of themselves, planets and moons on a plain dark ground, flags on a dark card, artworks on a dark wall with a paper mat. The cropped versions are offered under the same licences as their originals.

There are no photographs of people. Reels about people use name cards.

**Animals, landmarks and planets** come from the data files of [GCompris](https://gcompris.net) 4.0, the KDE educational suite, as packaged for Ubuntu (`gcompris-qt-data`). GCompris is published under the [GNU GPL, version 3 or later](https://www.gnu.org/licenses/gpl-3.0.html). Its package copyright file records these photos individually:

| Slide | Author | Licence | Source |
| --- | --- | --- | --- |
| Crocodile | Kmanoj | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Marsh_Crocodiles_basking_in_the_sun.JPG) |
| Komodo dragon | Raul654 | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Varanus_komodoensis4.jpg) |
| Koala | David Iliff | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Koala_climbing_tree.jpg) |
| Ring-tailed lemurs | Sannse | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Ring_tailed_lemur_and_twins.jpg) |
| Moose | Ryan Hagerty, U.S. Fish and Wildlife Service | Public domain | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Male_Moose.jpg) |
| Giant panda | Aaron Logan | [CC BY 1.0](https://creativecommons.org/licenses/by/1.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Lightmatter_panda.jpg) |
| Polar bear | Arturo de Frias Marques | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Polar_Bear_AdF.jpg) |
| Scarlet macaw | Jar0d | [CC BY-SA 2.0](https://creativecommons.org/licenses/by-sa/2.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Ara_macao_-Diergaarde_Blijdorp_-flying-8a.jpg) |
| The Louvre | Jean-Pierre Dalbéra | [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Le_mus%C3%A9e_du_Louvre_(4750261198).jpg) |
| The Leaning Tower of Pisa | Dan Kamminga | [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Torre_di_Pisa.jpg) |
| The Parthenon | Harrieta | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:2006_01_21_Ath%C3%A8nes_Parth%C3%A9non.JPG) |
| The Empire State Building | Lolalatorre | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Empire_State_Building_in_New_York.JPG) |
| The U.S. Capitol | Martin Falbisoner | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:US_Capitol_east_side.JPG) |
| Dome of the Rock | Andrew Shiva | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Israel-2013(2)-Jerusalem-Temple_Mount-Dome_of_the_Rock_(SE_exposure).jpg) |
| The Winter Palace | Dezidor | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) | [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Zimn%C3%AD_pal%C3%A1c_%283%29.jpg) |

The package gives no individual credit for the remaining photos; they are covered by GCompris's own GPL licence and credited to the GCompris contributors.

**Artworks** (the `art-*` slides) come from the same package: GCompris ships each one cut into jigsaw pieces for its paintings activity, and the slides here are those pieces put back together. The package credits the pictures to WebMuseum, under the GPL, version 3 or later. The works themselves are in the public domain: Hokusai (The Great Wave off Kanagawa, Ejiri in Suruga Province, Kazusa Sea Route, Sunset across Ryōgoku Bridge, Poppies, Oiran and Kamuro, Woman Holding a Fan), Hiroshige (Benzaiten Shrine at Inokashira in Snow, Horse Mackerel and Prawns), Leonardo da Vinci (Mona Lisa), Michelangelo (Pietà), Giovanni Bellini (a detail of the Pesaro Altarpiece), Albrecht Dürer (Lion), Pieter Bruegel the Elder (The Harvesters), Giuseppe Arcimboldo (Spring, The Librarian), Pierre-Auguste Renoir (Bal du moulin de la Galette, Girls at the Piano), Frédéric Bazille (The Ramparts at Aigues-Mortes), Mary Cassatt (Summertime), Vincent van Gogh (Village Street in Auvers) and Wassily Kandinsky (Composition VIII). Titles and attributions follow the package.

**Moons** (the Moon, Io, Europa, Ganymede, Callisto and Titan) are spheres drawn from the surface maps in [OpenUniverse](https://sourceforge.net/projects/openuniverse/) 1.0beta3 by Raúl Alonso, as packaged for Ubuntu (`openuniverse-common`), under the [GNU GPL, version 2 or later](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

**Flags** are from [flag-icons](https://github.com/lipis/flag-icons) 7.2.3 by Panayiotis Lipiridis, under the MIT licence, rendered to WebP.
