# Matrix reasoning puzzle generator

I built this to practise before a reasoning test, and then spent most of the time fixing the puzzles it produced rather than solving them.

It generates 3x3 matrix reasoning puzzles of the kind used in cognitive screening tests. Every puzzle is built from scratch when it appears, so you don't run out and you can't memorise the answers.

**Try it:** https://jakopx-berg.github.io/matrix-reasoning-generator/

## What this is

- One static HTML file, no dependencies, no login, no data collection.
- Eight puzzle types, each of which can be switched off, so you can drill one kind at a time.
- Three difficulty levels, which change how many rules stack inside a puzzle and which operators turn up, rather than just the time you get.
- Two modes. Learning mode marks your answer and explains the rule behind it. Exam mode gives you 60 seconds per item, no feedback along the way, and a score at the end.
- No item from any real test is reproduced. Everything is generated from rules written for this tool. Raven's Progressive Matrices and the commercial test batteries are copyrighted, and none of that material is here.

## The puzzle types

| Type | Rule |
|---|---|
| Distribution | Three shapes, each appearing once per row and column |
| Combination | The third cell overlays the first two |
| Shape + inner | Outer shape distributed, inner shape growing across the row |
| Quadrilateral + lines | The third figure combines the lines of the first two, by union, XOR, intersection or subtraction |
| Arrows | How many, the angle the bundle sits at, and where the heads are. Up to three rules at once |
| Rotation | A pointer turning a fixed step either way, sometimes with the surrounding shape distributing as a second rule |
| Dots | Counts by distribution, progression, addition or subtraction |
| Position | One or two markers travelling around the figure, each at its own rate and direction |

Several types have single-rule variants as well as two-rule ones, so the difficulty moves around between items.

## Making the items fair

The first version had a type where the answer came down to the size of an inner shape. The size did increase across the row, but the inner shape changed from cell to cell at the same time, so you were comparing a small triangle against a medium circle against a large diamond. Two of the six answer options differed by nothing else. It looked like a puzzle and wasn't one, because the feature that decided the answer couldn't be read off the page.

The fix was to hold the inner shape constant along each row so the comparison is like for like, and to widen the size steps to about two and a half times from smallest to largest.

The second round came from the items feeling repetitive. Two things caused it. Type selection was uniform random, which streaks and hands you the same kind four times running. And every type at that point drew one shape inside another, so they resembled each other whatever the underlying rule was. Selection now rotates through a shuffled bag, so no type repeats back to back and each comes up equally often. The types added later were drawn to look different from one another.

A third round went into the wrong answers rather than the puzzles. Random wrong options are easy to dismiss, because you can often see which ones belong to the family without solving anything. The options are now built deliberately: the result of stopping one step short or going one step too far, the correct figure with exactly one attribute changed, a straight copy of a neighbouring cell, and for the line puzzles the result of every other logical operator applied to the same two figures. That last one does the most work. If the rule is XOR, the union of the two figures is sitting right there among the options, looking reasonable.

There is a fourth thing worth saying, because it decided what the difficulty setting is allowed to do. A matrix item can be made harder in two quite different ways: by adding relations you have to hold and combine at once, or by making the difference on screen harder to notice. Only the first is the thing these tests set out to measure. So turning the difficulty up stacks more rules into an item and reaches for the harder operators, and it deliberately leaves the rotation step alone. Turning a pointer 45 degrees instead of 90 makes the change harder to see while the rule behind it stays exactly as simple. Rotation earns its difficulty by picking up a second rule instead.

Each generator is checked over tens of thousands of runs before it ships: six unique options, exactly one correct, and the stated rule actually determining the answer in every cell of the grid.

## Running it locally

Open `index.html` in a browser. That is the whole installation.

## License

MIT. See [LICENSE](LICENSE).

Built with agentic AI tools. Made by Jakop Berg, September 2026.
