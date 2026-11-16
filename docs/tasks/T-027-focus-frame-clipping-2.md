# T-027 Focus frame cut off in movie, series, cast and sport screens

Follow-up to T-026. Same cause: lists and grids clip to their own bounds, so the enlarged focused item and its shadow need room in the content padding. Found by reading the code; not reproduced on a device.

## Changes

| Place | Before | After |
|---|---|---|
| `BrowseScreen.kt` movie/series grid | no side padding, 14 dp above | 16 dp at the sides, 28 dp above; `cardW` now subtracts the side padding so the covers still fit the cells |
| `CategoriesScreen.kt` preview grid (left open in T-026) | no side padding, 24 dp above/below | 16 dp sides, 28 dp above/below; `byWidth` subtracts 32 dp |
| `DetailScreen.kt` episode list | no side/top padding, scale origin at the left edge (all growth to the right, clipped) | default origin, 16 dp sides, 12 dp above |
| `DetailScreen.kt` season list | no side padding | 10 dp sides, 12 dp above/below |
| `CastUi.kt` cast, similar titles, person's titles | 16-18 dp above/below | 22 dp |
| `SportHub.kt`, `SportLeague.kt` match rows | 8-10 dp above/below | 14 dp |

## Not changed
- Sport rows have no side padding of their own (they sit inside a padded list). Left as is, alignment would shift.
- The expanded "scene image" card in the movie grid (right columns open to the left) was not checked.
- Scale factors, shadow size, texts, storage.

## Acceptance criteria
1. Movies/series grid: focus first and last column, first and last row; frame and shadow complete.
2. Categories, preview grid: same check.
3. Series detail: move through episodes and seasons; frame complete at the right and left.
4. Cast and similar-title rows: first and last card complete.
5. Sport hub / league rows: shadow of the match cards complete above and below.

## Checks
Not built, not tested on a device (no Kotlin compiler here). Parameter values only. **Unverified** on the device.
