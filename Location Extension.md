# Optional PAOL / PAO+L Extensions

A conventional two-digit PAO encodes six digits per complete scene:

```text
PP + AA + OO = 6 digits
```

A further **Location** component may extend the scene horizontally:

```text
P + A + O + L
```

There are two approaches to that:
- one easier and more convenient but also less natural: creating a seven-digit **PAO+L** scene when Location encodes one additional digit
- and another more difficult to learn but more natural: creating a full eigth-digit **PAOL** scene when Location encodes two additional digits

This Location digit(s) is not a third digit of the Person code and should not be confused with the optional hierarchical `XYZ` Person extension described earlier.

## Option A: Coding just one digit: PAO+L 

An easy implementation is to associate Location classes with the same broad semantic structure used by the Person categories:

```text
0   stage
1   atelier
2   ancient world
3   graphic world
4   nature
5   otherworld
6   city
7   factory
8   arena
9   village
```

Suggested interpretations:

**0 --- Stage**
Concert stage, theatre stage, performance venue, backstage, rehearsal
stage, cabaret stage, television performance stage, outdoor stage,
auditorium; indoor scenery

**1 --- Atelier**
Artist's studio, painter's studio, sculptor's studio, photography
studio, writer's study, library, gallery, music room, film studio; indoor scenery

**2 --- Ancient World**
Ruins, temple, colonnade, amphitheatre, ancient palace, sacred grove,
ancient harbor, rocky Mediterranean landscape, legendary landscape; outdoor scenery

**3 --- Graphic World**
A coherent stylized graphic environment using the rendering rules
defined in Section 15; either indoor or outdoor scenery

**4 --- Nature**
Forest, meadow, mountains, rocky landscape, jungle, desert, coast,
riverbank, park, snowy landscape; outdoor scenery

**5 --- Otherworld**
Alien planet, outer space, spacecraft environment, magical realm,
fantasy landscape, surreal landscape, underground realm, impossible
architecture; either indoor or outdoor scenery

**6 -- City**
City street, public square, civic building, palace, castle, parliament
district, monumental avenue, courtyard, city gate, urban park; outdoor scenery

**7 --- Factory**
Workshop, machine shop, factory floor, engineering laboratory,
electronics laboratory, industrial hall, power plant, garage, technical
workbench; indoor scenery

**8 --- Arena**
Stadium, running track, boxing ring, tennis court, football pitch,
basketball court, gymnastics hall, ice rink, racing circuit, training or
competitive venue; indoor scenery

**9 --- Village**
House, garden, residential street, neighborhood, small-town square,
railway station, farm, local shop, country road, ordinary workplace; outdoor scenery


## Option B: Coding full two digits: PAOL

It extends semantically entire system, effectively requiring creation of 100 different locations. They should be distinct enough and - per the way the PAO system is created - in this "mode" they should rely more on association with the person instelf rather than its category.

The assignement architecture would follow the relationship presented below:

```text
P <-> L
```

In any case the Location layer is optional. Its purpose is to increase scene capacity while keeping the additional information in a perceptually different channel from Person, Action, and Object.


# Proposed additions to PAO Grammar

------------------------------------------------------------------------

## 9. Location classes

The first digit/category determines the Location class:

  Category   Location class      Core semantic domain
  ---------- ------------------- ----------------------------------------------
  0          **Stage**           performance
  1          **Atelier**         artistic creation
  2          **Ancient World**   antiquity, myth, legend
  3          **Graphic World**   unified graphic reality
  4          **Nature**          predominantly non-built natural environment
  5          **Otherworld**      fantastic, alien, impossible reality
  6          **City**            civilization, history, political power
  7          **Factory**         technology, engineering, functional creation
  8          **Arena**           competition
  9          **Village**         ordinary everyday world

These are **families of locations**, not fixed backgrounds.

------------------------------------------------------------------------

## 10. Location vocabulary

### 0 --- Stage

Concert stage, theatre stage, performance venue, backstage, rehearsal
stage, cabaret stage, television performance stage, outdoor stage,
auditorium.

### 1 --- Atelier

Artist's studio, painter's studio, sculptor's studio, photography
studio, writer's study, library, gallery, music room, film studio.

### 2 --- Ancient World

Ruins, temple, colonnade, amphitheatre, ancient palace, sacred grove,
ancient harbor, rocky Mediterranean landscape, legendary landscape.

### 3 --- Graphic World

A coherent stylized graphic environment using the rendering rules
defined in Section 15.

### 4 --- Nature

Forest, meadow, mountains, rocky landscape, jungle, desert, coast,
riverbank, park, snowy landscape.

### 5 --- Otherworld

Alien planet, outer space, spacecraft environment, magical realm,
fantasy landscape, surreal landscape, underground realm, impossible
architecture.

### 6 --- City

City street, public square, civic building, palace, castle, parliament
district, monumental avenue, courtyard, city gate, urban park.

### 7 --- Factory

Workshop, machine shop, factory floor, engineering laboratory,
electronics laboratory, industrial hall, power plant, garage, technical
workbench.

### 8 --- Arena

Stadium, running track, boxing ring, tennis court, football pitch,
basketball court, gymnastics hall, ice rink, racing circuit, training or
competitive venue.

### 9 --- Village

House, garden, residential street, neighborhood, small-town square,
railway station, farm, local shop, country road, ordinary workplace.

------------------------------------------------------------------------

## 11. Location selection

Within the required Location class, choose the subtype according to this
priority:

**semantic reinforcement \> naturalness \> card distinctiveness \>
variation**

A background may deliberately reinforce Person, Action, or Object.

Example:

**Object = tree + Location = Nature → forest is desirable**

Semantic redundancy is not a problem. A Location is secondary in
**visual salience**, not necessarily secondary in semantic relevance.

------------------------------------------------------------------------