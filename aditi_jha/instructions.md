# Driftwood Arcade Browser Game Portal

**Category:** Web Development

**Project type:** Responsive multi page gaming website with three browser games

---

## 1. Project Context

Driftwood Arcade is a small independent studio that makes light hearted pixel art
games for the web. The studio has released a few short game jam entries but has
no public website yet, no fixed brand palette, and no single place to show its
games. This project builds that home: a portal where a visitor can land, browse a
catalogue of games, open a game, play a round in the browser, and check a high
score board, all in one short visit.

The whole site is a static front end project. It runs on HTML, CSS, and plain
JavaScript only. There is no backend, no database, and no account system. Game
scores are stored inside the browser using local storage. The catalogue of games
is loaded from a supplied JSON dataset so the studio can add more games later by
editing data instead of editing pages.

This milestone is the full website plus three playable games. It is not a native
app, not a multiplayer service, and not a content management system.

---

## 2. Software Stack

1. HTML5 for structure.
2. CSS3 for layout and theme. Plain CSS or a single CSS file set. CSS variables
   are allowed.
3. Vanilla JavaScript (ES6) for the catalogue, the games, the leaderboard, and
   the form. No frameworks and no libraries.
4. The HTML5 Canvas element and its 2D context for the three games.
5. The local storage browser API for saving high scores.
6. The fetch API for loading the games dataset from `assets/games.json`.

Not allowed: React, Vue, Angular, Svelte, jQuery, Bootstrap, Tailwind, any build
tool or bundler, any paid plugin, any paid font, and any backend or database.

Browser support: the site works in the latest versions of Chrome, Edge, Firefox,
and Safari.

---

## 3. Site Pages and Navigation

The site has six page types across eight HTML files. Every page shares the same
header navigation and the same footer.

| Page | File name | Purpose |
|---|---|---|
| Home | `index.html` | Intro, featured games, link into the catalogue |
| Catalogue | `games.html` | Grid of all games from the dataset, filter and search |
| Game page | `dune-dash.html`, `star-catcher.html`, `tide-match.html` | One page per playable game with the canvas and rules |
| High scores | `leaderboard.html` | Best score per game from local storage |
| About | `about.html` | Studio story and the three game descriptions |
| Contact | `contact.html` | Styled contact form with browser side validation |

### Header navigation

- The header shows the text logo `DRIFTWOOD ARCADE` on the left.
- The header shows links to Home, Games, Scores, About, and Contact. The Scores
  link opens `leaderboard.html`, which is the high score board.
- The link for the current page is shown in the secondary accent colour.
- On screens 600 pixels wide or narrower the links collapse behind a menu button
  that opens and closes the link list on tap.

### Footer

- The footer shows the text `Driftwood Arcade` and the line `Made for play`.
- The footer is the same on every page.

---

## 4. Visual Theme

The studio has no existing palette, so the palette below is the one to use. Tone
is playful, retro, and pixel flavoured.

### Colours

| Purpose | Name | Hex |
|---|---|---|
| Page background | Midnight | `#161A2B` |
| Panels and cards | Surface | `#232845` |
| Primary accent (buttons, highlights) | Sand | `#F4A259` |
| Secondary accent (active links, focus) | Tide | `#4ECDC4` |
| Primary text | Foam | `#F5F6FA` |
| Muted text | Mist | `#9AA0BF` |
| Loss and errors | Coral | `#E15A5A` |
| Win and success | Kelp | `#6FCF6B` |

Colour rules:

1. Use only the eight colours above plus pure black and pure white.
2. Buttons use the Sand background with Midnight text.
3. Links and active states use the Tide colour.
4. Error messages use the Coral colour.

### Typography

| Usage | Font | Notes |
|---|---|---|
| Logo and headings | `Press Start 2P` | Pixel display font under the SIL Open Font License. Fallback `"Courier New", monospace` |
| Body and buttons | System sans stack `"Segoe UI", Roboto, Helvetica, Arial, sans-serif` | Base size 16 pixels, line height 1.5 |

Typography rules:

1. The heading font is `Press Start 2P`. Any other pixel display font under the
   SIL Open Font License is an accepted substitute, and the `monospace` fallback
   is required either way.
2. The heading font and the body font are visibly different.
3. Body text is never smaller than 14 pixels.
4. No paid font is used.

### Layout and sizing

1. The centred content area is at most 1100 pixels wide.
2. The header is 64 pixels tall on desktop.
3. Card corners use a 10 pixel radius. Panels use a 14 pixel radius.
4. Spacing between cards in any grid is 20 pixels.

---

## 5. Games Catalogue and Dataset

The catalogue page `games.html` is built from the dataset file
`assets/games.json`. The page loads the dataset with fetch and renders one
card per game. The cards are not written into the HTML by hand.

### Dataset

The dataset is supplied in `assets/games.json`. Each game record holds these
fields:

- `id`: short lowercase id with hyphens.
- `title`: display name.
- `slug`: same as the id, used for the page file name.
- `category`: one of `Action`, `Arcade`, `Memory`, `Puzzle`.
- `status`: `playable` or `coming_soon`.
- `page`: the game page file name, or an empty string when coming soon.
- `thumbnail`: path to the card image inside `assets/sprites`.
- `short_description`: one line shown on the card.
- `controls`: one line describing the controls.
- `difficulty`: `Easy`, `Medium`, or `Hard`.
- `tags`: a list of short tag words.
- `highscore_key`: the local storage key that holds the best score, or an empty
  string when coming soon.

The dataset ships with six records. Three records have `status` set to
`playable` (Dune Dash, Star Catcher, Tide Match) and three have `status` set to
`coming_soon`.

### Catalogue card

Each card shows the thumbnail, the title, a category badge, the difficulty, and
the short description. A card whose status is `playable` shows a Play button that
links to the game page. A card whose status is `coming_soon` shows a muted
`Coming soon` label and no Play button.

### Filter and search

1. A category filter offers `All`, `Action`, `Arcade`, `Memory`, and `Puzzle`.
   Selecting a category shows only the matching cards. `All` shows every card.
2. A text search box filters the cards by matching the typed text against the
   game title, ignoring letter case.
3. The filter and the search work together on the same dataset in the browser.
4. When no card matches, the page shows the line `No games match that filter`.

---

## 6. Game One: Dune Dash

A one button endless jumper rendered on a canvas.

1. The game page is `dune-dash.html` and the canvas is 800 pixels wide by 300
   pixels tall.
2. A character sits on a ground line on the left side of the canvas.
3. Obstacles enter from the right edge and move left at a starting speed.
4. The Space key, the Up arrow key, and a tap or click on the canvas each make
   the character jump. The character cannot jump again until it lands.
5. When the character touches an obstacle the run ends.
6. The score counts up by 1 for every obstacle that passes the character.
7. The obstacle speed increases after every 5 obstacles passed. The step is a
   fixed amount chosen by the developer, stays constant for the whole run, and is
   visible in play.
8. On game over the canvas shows the final score, the best score, and a Restart
   button or a Restart key prompt.
9. The best score is saved to local storage under the key
   `driftwood_dune_dash_best`. A higher score replaces the stored value.

---

## 7. Game Two: Star Catcher

A falling object catcher rendered on a canvas.

1. The game page is `star-catcher.html` and the canvas is 600 pixels wide by 400
   pixels tall.
2. A basket sits near the bottom and moves left and right with the Left arrow
   key and the Right arrow key. The basket also follows the pointer when the
   pointer moves across the canvas.
3. Stars fall from the top at random horizontal positions.
4. Bombs also fall from the top at random horizontal positions.
5. Catching a star adds 1 to the score.
6. Catching a bomb removes 1 life. The game starts with 3 lives.
7. The fall speed increases as the score rises. The rate is chosen by the
   developer and stays consistent within a run.
8. The run ends when lives reach 0. The canvas then shows the final score, the
   best score, and a Restart button or a Restart key prompt.
9. The best score is saved to local storage under the key
   `driftwood_star_catcher_best`. A higher score replaces the stored value.

---

## 8. Game Three: Tide Match

A memory match game rendered on a canvas or with positioned elements.

1. The game page is `tide-match.html` and the board is a four by four grid of 16
   cards, which is 8 matching pairs.
2. Each card starts face down. The eight pair icons come from the supplied
   sprite set in `assets/sprites`.
3. Clicking or tapping a face down card turns it face up.
4. When two cards are face up the game checks them. A matched pair stays face up.
   A mismatch turns both cards face down again after a pause of about 1 second.
5. The board shuffles the card positions at the start of every new game.
6. A moves counter increases by 1 each time a second card of a pair is turned up.
7. The game ends when all eight pairs are matched. The board then shows a win
   message and the moves used.
8. The fewest moves result is saved to local storage under the key
   `driftwood_tide_match_best`. A lower number of moves replaces the stored value.
9. A New Game button reshuffles the board and resets the moves counter.

---

## 9. High Score Board

The page `leaderboard.html` reads the three best score keys from local storage
and shows them in one table.

1. The table has three rows, one for Dune Dash, one for Star Catcher, and one for
   Tide Match.
2. Each row shows the game name, the score label, and the stored value.
3. The score label for Dune Dash and Star Catcher is `Best score`. The score
   label for Tide Match is `Fewest moves`.
4. When a key has no stored value yet the row shows a dash character in the value
   column.
5. The page reads the same local storage keys named in sections 6, 7, and 8.

---

## 10. Contact Page

The page `contact.html` holds a styled contact form. The form never sends data
to any server.

1. The form has a Name field, an Email field, and a Message field.
2. All three fields are required.
3. The Email field is checked against an email pattern that requires text, an at
   sign, a domain, and a dot, for example `name@example.org`.
4. The Message field requires at least 10 characters.
5. On submit the page prevents the default browser submit.
6. When any field is invalid the form shows an inline error message in the Coral
   colour next to that field.
7. When all fields are valid the page hides the form and shows the confirmation
   line `Thanks for reaching out to Driftwood Arcade`.

---

## 11. Responsive Behaviour

1. The site works from a 320 pixel wide screen up to a wide desktop.
2. At 600 pixels wide or narrower the header links collapse behind a menu button.
3. The catalogue grid shows one column at 600 pixels or narrower, two columns
   between 601 and 1024 pixels, and three columns above 1024 pixels.
4. Each game canvas scales down to fit its container width on small screens while
   keeping its width to height ratio.
5. No horizontal scrollbar appears at any width from 320 pixels upward.

---

## 12. Assets and References

1. The reference image `reference_image.png` in the project root shows the home
   page and catalogue layout. Match the structure, the page order, and the theme.
   Small spacing changes are allowed.
2. The games dataset is `assets/games.json`.
3. The studio logo is `assets/sprites/logo.png`, supplied for brand reference.
   The header keeps the text logo, and the logo image may sit beside it.
4. The square logo emblem is `assets/sprites/logo-mark.png`. It can be used as a
   favicon or a small badge. Using it is optional.
5. The card thumbnails and the game sprites are in `assets/sprites`. These are
   copyright free and free to use.
6. Any extra art added must also be copyright free. Recolouring the supplied
   sprites is allowed. Adding paid or branded art is not allowed.

How to use the reference image: treat it as the layout guide for spacing, page
order, and theme. Where the reference and a written rule in this file disagree,
follow the written rule.

---

## 13. Deliverables

| # | Item | Format | Notes |
|---|---|---|---|
| 1 | Home page | `index.html` | Header, featured games, footer |
| 2 | Catalogue page | `games.html` | Cards from the dataset, filter, search |
| 3 | Game page Dune Dash | `dune-dash.html` | Canvas game from section 6 |
| 4 | Game page Star Catcher | `star-catcher.html` | Canvas game from section 7 |
| 5 | Game page Tide Match | `tide-match.html` | Memory game from section 8 |
| 6 | High score board | `leaderboard.html` | Table from section 9 |
| 7 | About page | `about.html` | Studio story and game descriptions |
| 8 | Contact page | `contact.html` | Form from section 10 |
| 9 | Styles | `.css` | One or more CSS files for the theme |
| 10 | Scripts | `.js` | Catalogue, games, leaderboard, form logic |
| 11 | Dataset | `assets/games.json` | The games dataset, kept in place |
| 12 | Assets | `assets/sprites/` | The supplied copyright free art, kept in place |
| 13 | README | `README.md` | How to run the site on a local static server |

### File naming convention

1. All HTML, CSS, and JavaScript file names use lowercase letters.
2. Words in a file name are joined with hyphens, for example `star-catcher.html`.
3. No spaces and no capital letters appear in any delivered file name, except the
   README file which is named `README.md`.

### Folder structure

```
driftwood-arcade/
  index.html
  games.html
  dune-dash.html
  star-catcher.html
  tide-match.html
  leaderboard.html
  about.html
  contact.html
  css/
    style.css
  js/
    main.js
    catalogue.js
    dune-dash.js
    star-catcher.js
    tide-match.js
    leaderboard.js
    contact.js
  assets/
    games.json
    sprites/
  README.md
```

The exact split of JavaScript files is open as long as each page loads only the
scripts it needs and the catalogue reads the dataset from `assets/games.json`.

---

## 14. Code Quality

1. The HTML validates with no unclosed tags.
2. The browser console shows no errors when each page loads and when each game
   is played from start to game over.
3. CSS, HTML, and JavaScript are split into separate files. No inline style
   attributes are used for layout.
4. Functions and variables have names that describe what they do.
5. Each script file holds a short comment block at the top that names the page it
   serves.

---

## 15. Scope Boundaries

### DO

1. Build all six page types and the three games described above.
2. Load the catalogue from `assets/games.json`.
3. Save and read scores with local storage using the keys named above.
4. Use the supplied copyright free sprites, or recolour them.
5. Keep the whole project static and runnable from a static file server.

### DO NOT

1. Do not add a backend, a database, or a login system.
2. Do not add multiplayer, online leaderboards, or chat.
3. Do not add payment, advertising, or purchase features.
4. Do not use any framework, bundler, or paid plugin.
5. Do not use paid or branded art or paid fonts.

---

## 16. Acceptance Gates

The delivery passes only when every gate below is true.

1. All eight pages from section 13 are present and link to each other through the
   shared header.
2. The catalogue renders its cards from `assets/games.json` using fetch.
3. The category filter and the title search both work on the catalogue.
4. Dune Dash runs, ends on collision, and stores the best score under
   `driftwood_dune_dash_best`.
5. Star Catcher runs, ends at 0 lives, and stores the best score under
   `driftwood_star_catcher_best`.
6. Tide Match ends when all pairs match and stores the fewest moves under
   `driftwood_tide_match_best`.
7. The leaderboard shows the three stored values and a dash when a value is
   missing.
8. The contact form validates its three fields and shows the confirmation line on
   a valid submit.
9. The layout shows no horizontal scrollbar from 320 pixels wide upward and the
   header collapses at 600 pixels or narrower.
10. The browser console shows no errors during normal use.
11. The README explains how to run the site on a local static server.

---

## 17. Evaluation Criteria

1. All eight pages exist, share one header and footer, and use the section 4
   palette and typography.
2. The catalogue is data driven from `assets/games.json` with a working filter
   and search.
3. Each of the three games meets its rules in sections 6, 7, and 8, including the
   canvas size and the local storage key.
4. The leaderboard reads the three keys and handles missing values.
5. The contact form validates all three fields and confirms on valid submit.
6. The layout is responsive from 320 pixels with a collapsing menu at 600 pixels.
7. The code is split into separate files, runs with no console errors, and uses
   descriptive names.

---

## 18. Delivery Terms

1. This is a single delivery. Up to one round of minor revisions may be requested,
   and a revision only covers the acceptance gates in section 16.
2. A revision does not include new games, new pages, or any change to the rules in
   this file.
3. The estimated effort is 12 to 18 hours of work.
4. The handover is the complete source folder of HTML, CSS, JavaScript, the
   dataset, the assets, and the README, delivered as one archive that runs when
   served from a static file server.
