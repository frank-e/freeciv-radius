# freeciv-radius
*Freeciv ruleset with a built-in tutorial by [dunnoob](https://freeciv.fandom.com/wiki/User:Dunnoob "dunnoob")*.

```
 The radius ruleset is based on the classic Freeciv rules
 adopting many ideas from the experimental and civ2civ3
 rulesets.  It features a growing city radius_sq from 4
 to 20:
    size   radius (sq.)   vision  squares (hexes)
       1    4 = 2*2 + 0*0      5       13 (19)
       4    5 = 2*2 + 1*1      8       21 (19)
       9    8 = 2*2 + 2*2      9       25 (19)
      16    9 = 3*3 + 0*0     10       29 (37)
      25   10 = 3*3 + 1*1     13       37 (37)
      36   13 = 3*3 + 2*2     16       45 (37)
      49   16 = 4*4 + 0*0     17       49 (61)
      64   17 = 4*4 + 1*1     18       57 (61)
      81   18 = 3*3 + 3*3     20       61 (61)
     100   20 = 4*4 + 2*2     25       69 (61)
```

1. Download version 2.5.1 released as [Last known good state 2019](https://github.com/frank-e/freeciv-radius/releases/tag/v2.5.1 "2.5.1").
2. Download version 2.6.1 pre-released as [2017.07.11](https://github.com/frank-e/freeciv-radius/releases/tag/v2.6.1 "2.6.1").

## Terrain ##
### Glacier ###
In the standard rulesets (classic, experimental, civ2civ3) the transformation
of mountains to plains takes 48 move points, e.g., 24 turns for one engineer.
The transformation of a glacier to plains takes 72 move points (36 turns for
one engineer).  This difference (24 move points) also affects transformations
to grassland (72 vs. 96) or ocean (114 vs. 138), among others.

Arguably glaciers are too hard.  One way to fix this is a new transformation
of tundra to swamp instead of desert (24 move points, as for all other land
to land transformations in the standard rulesets).  With this modification
the transformation of a glacier over swamp to forest or grassland takes 63
move points (instead of 87 or 96 over desert and plains).  A transformation
to ocean or lake via swamp takes 96 instead of 138 move points.

The introduction of mining on tundra resulting in a desert (15 move points,
as for various other mining operations) permits to reach plains in 63 instead
of 72 move points.  It also preserves the fast resurrection of an oil mine on
desert after global warming transformed a glacier with oil mine to a tundra
without mine.

### Jungle ###
In the standard rulesets (classic, experimental, civ2civ3) most terrain forms
can be reached as the result of intentional transformations.  Some exceptions
are glacier, mountains, deep ocean, and jungle.  This is an issue when global
warming or nuclear winter transform terrain tiles with special resources, and
engineers are supposed to "repair" the damage.  Global disasters don't affect
deep ocean, hills, and mountains.  Other terrain forms (including glacier and
jungle) are vulnerable.  A lost arctic oil mine can be resurrected as desert
oil mine, but lost arctic ivory is definitely gone (actually a nuclear winter
could "undo" this effect of an earlier global warming).  Likewise any special
resources (gems or fruit) on transformed jungle tiles are definitely gone.

In addition to its vulnerability an engineering transformation of jungle to
plains takes 24 move points, but an ordinary transformation by workers or
settlers to plains via forest takes only 20 move points.  One way to fix both
issues with jungles is to shuffle some transformations:  The transformation
result for forest can be jungle instead of grassland.  It is still possible
to reach grassland from forest via swamp (15+15 instead of 24 move points)
or via plains (5+24).  In the standard rulesets jungle is already one of the
possible transformation results for forests caused by global warming.

The transformation result for jungle can be tundra instead of grassland for
similar reasons.  This allows to "repair" global warming damages of special
resources on tundra (furs or game).

### Marina ###
Marinas add a port facility to an existing fortress and require an adjacent
lake or ocean.  Among other effects, a sea unit remaining in a marina for a
whole turn without moving recovers a quarter of its hit points (same idea as
for land units in a fortress).  Sea units in a marina may be attacked by land
units.

### Deep Ocean ###
Buoys can be built on lakes and shallow ocean tiles, but not on deep ocean
"floor" tiles.  Offshore Platforms cannot be built on Deep Ocean tiles.  The
map generators never creates Deep Ocean tiles with adjacent land tiles, but
later terrain modifications can change this.

### Rivers ###
Cities on rivers or with an adjacent oceanic tile can be hit by a flood.  As
in the classic ruleset it is possible to build a fortress on a tile with a
river.  Found in the experimental ruleset:  Triremes can move on rivers.

### Tramway ###
In this ruleset a new tramway replaces the classic railroad with movecost 10
to get 60/10 MP for 60 fragments.  A new railroad has cost 5 for 60/5 MP,
and can be build on tiles with tramways.  Building a raiload takes the same
time as building a road (terrain-specific slower).  The Railroad technology
permits to build tramways and railroads with automatical tramways on city
center tiles.

The movecost for roads and rivers is 20 for 60/20 MP; this corresponds to
the classic triple speed.  There is no zero cost "infinite" move speed as
for the classic railroad or the experimental maglev.

CAVEATS:  Any veteran_move_bonus in the units.ruleset has to be adjusted for
a new number of move_fragments in the terrain.ruleset.

### Gold ###
 *Not up to date, maybe not yet working as expected (=stay below 10)*
In this ruleset the trade bonus for gold is 5, or 7 with a tramway (150%).
Railroads add 20% to any shield or trade bonus; this affects bonus 3 or 5:
170% of 1, 2, or 4 is still 1 (1.7), 3 (3.4), or 6 (6.8); but 170% of 3 is
5 (5.1) instead of the standard 4 (4.5).

Railroads on mountains with gold yield 8 (8.5) trade points for 170% of 5
instead of the standard 9.  This is also nice for tilesets with no bonus 10
graphics, e.g., gold rivers with a railroad (standard: 10, this ruleset: 9).

### Frigate ###
Caravels are obsoleted by frigates, and frigates are obsoleted by transports.
Frigates can be converted (downgraded) to galleons.  Galleons cannot attack,
but can carry 4 instead of 2 units.

TBD:  convert_time = 3 did not work as expected (3 turns) in a v2.5.6 test.

### Trade ###
The 1st trade route requires a Marketplace, Bank, or Stock Exchange.  Further
trade routes require two of these buildings.  The discovery of Magnetism or
the Corporatation permits a 3rd trade route.  Both techs permit a 4th trade
route.

Intercontinental trade routes get a 167% value.  International trade routes
(even with enemies) get a 133% value.  The combined INIC value is (only) 200%
to discourage overzealous AIs.

The permanent trade value is mutual, both cities connected by a trade route
get the same trade points.  The initial bonus for a new trade route is not
shared by the target city.  The discovery of Railway or Flight by the nation
of the source city reduce the initial bonus for new trade routes.

TBD:  Why is the magic number for both reductions 585 in some rulesets, and
is this wrong for the non-standard IN/IC/INIC factors here?
