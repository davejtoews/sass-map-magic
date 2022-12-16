# Sass Map Magic
A sass utility library for handling [map values](https://sass-lang.com/documentation/values/maps). The functions here take maps as one or more of their arguments and return new modified map values.

## Arithmatic
Included are five functions corresponding to five [numeric operators](https://sass-lang.com/documentation/operators/numeric): `add()`, `subtract()`, `mutiply()`, `divide()` and `modulo()`. The first two arguments can be map values or single values. All except `modulo()` accept a 3rd boolean argument to toggle the return value as a css `calc()` string rather than the result of sass arithmetic. (CSS calc does not support modulo).

If using two map values, both must have identical key values.

### Example - Map by single value

```scss
@use "~sass-map-magic" as magic;

$map: (
    "phone": 10px,
    "tablet": 20px,
    "desktop": 30px
);

$newMap = magic.multiply($map, 2);

//result
$newMap: (
    "phone": 20px,
    "tablet": 40px,
    "desktop": 60px
);
```

### Example - Map by map with calc

```scss
@use "~sass-map-magic" as magic;

$map: (
    "phone": 10px,
    "tablet": 20px,
    "desktop": 30px
);

$modifier: (
    "phone": 1vw,
    "tablet": 2vw,
    "desktop": 3vw
);

$newMap = magic.add($map, $modifier, true);

//result
$newMap: (
    "phone": calc(10px + 1vw),
    "tablet": calc(20px + 2vw),
    "desktop": calc(30px + 3vw)
);
```

## Slice

Slice can be used to return a segment of an existing map, taking the start and end key as arguments

### Example

```scss
@use "~sass-map-magic" as magic;

$map: (
    "phone": 10px,
    "large-phone": 15px,
    "tablet": 20px,
    "desktop": 30px,
    "desktop-large": 40px
);

$newMap = magic.slice($map, 'large-phone', 'desktop');

//result
$newMap: (
    "large-phone": 15px,
    "tablet": 20px,
    "desktop": 30px
);
```