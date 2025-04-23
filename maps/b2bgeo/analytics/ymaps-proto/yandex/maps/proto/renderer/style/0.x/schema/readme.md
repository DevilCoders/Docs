# Style spec for vector rendering clients

The main goal of this spec is to define a way to describe styling of arbitrary geographical data.
This styling format allows to:
* change styling and data protocols independently. This helps to replace expensive support of multiple tile set versions with support of multiple style versions.
* use arbitrary data, such as geojson, vector tiles or sets of map objects.
In order to achieve these goals, the requirements on the dataset should be sparse. This style spec is based on the following assumptions:
1) A dataset contains point, polyline, polygon features with named attributes.
2) Features in a dataset might be divided into named collections a.k.a 'source layers'

The root message is Style. Style is composed of multiple Layers, which should be rendered in order of appearance.
Each layer has:
* a filter that defines which features from data source participate in rendering of this particular layer(see Expression)
* a layer style that defines a visual style of the layer. Some styles are 'data-driven': evaluated as the result of an Expression that 
uses object attributes or current zoom.

## On point label styling

Abundance of point labeling styling properties might lead to confusion without visual explanation.
Following diagram covers text and icon position relative to feature.

```
//
//                       +---------------+
//                       |    ,-' `-.    |
//                       |  ,'       `.  |
//                       | ,           . |         +------+
// text anchor ----------+-+---> *     | +<------->+ TEXT |
// position is set by    |  \         /  |    ^    +------+
// text-anchor-icon-pos  |   .       .   |    |
//                       |    \     /    |    +---- text-offset adjusts distance from text to text
//                       |     .   .     |          anchor or icon(in case offset-from-icon is enabled)
//                       |      \ /      |
//                       |       * <-----+--------- feature position relative to the icon is set
//                       +---------------+          by icon-offset
//
```


## Expressions:

### get
Retrieves a property value from feature's properties.
Returns null if the requested property is missing.

#### Syntax
```
["get", string]: value
```

### has, !has
Checks if property is present(not present) among feature's properties.

#### Syntax
```
["has"|"!has", string]: boolean
```

### in, !in
Determines whether an item is in(not in) an array or a substring is in(not in) a string.

#### Syntax
```
["in"|"!in",
  keyword: InputType (boolean, string, or number),
  input: InputType (array or string)
  ]: boolean
```

### contains-any, contains-all, contains-none
Determines whether array contains any(all, none) of the items of array given as a second argument.

#### Syntax
```
["contains-(any|all|none)",
  input: InputType (array<number> or array<string>),
  values: InputType
]: boolean
```

### !
Returns true if the input is false, and false if the input is true.

#### Syntax
```
["!", boolean]: boolean
```

### ==, !=, <, >, <=, >=
Evaluates binary boolean expression.

#### Syntax
```
["=="|"!="|"<"|">"|"<="|">=", value, value]: boolean
```

### +, -, *, /
Evaluates a standard binary math expression.

#### Syntax
```
["+"|"-"|"*"|"/", number, number]: number
```

### %
Evaluates the remainder of the division operation `x/y`, where `x` is the first argument of this expression, and `y` the second.

The remainder of the division operation `x/y` calculated by this expression is exactly the value `x - n*y`, where `n` is `x/y` with its fractional part truncated.

The returned value has the same sign as x and is less than y in magnitude. 

#### Syntax
```
["%", number, number]: number
```

### ^
Evaluates the value of the first argument raised to the power of the second argument.

#### Syntax
```
["^", number, number]: number
```

### min, max
Returns the smaller or larger of two arguments, treating NaNs as missing data (between a NaN and a numeric value, the numeric value is chosen).

#### Syntax
```
["min"|"max", number, number]: number
```

### all, any, none
Returns true if all(any, none of) the inputs are true, false otherwise. The inputs are evaluated in order, and evaluation
finishes once the result may be deduced.

#### Syntax
```
["all"|"any"|"none", boolean, ...]: boolean
```

### case
Selects the first output whose corresponding test condition evaluates to true, fallback value otherwise.

#### Syntax
```
["case",
  condition: boolean, output: OutputType,
  condition: boolean, output: OutputType,
  ...,
  fallback: OutputType
]: OutputType
```

### match
Selects the output whose label value matches the input value, or the fallback value if
no match is found. The input can be any expression (e.g. ["get", "building_type"]). Each label must be either:
* a single literal value; or
* an array of literal values, whose values must be all strings or all numbers

#### Syntax
```
["match",
  input: InputType (number or string),
  label: InputType | [InputType, InputType, ...], output: OutputType,
  label: InputType | [InputType, InputType, ...], output: OutputType,
  ...,
  fallback: OutputType
]: OutputType
```

### interpolate
Produces continuous, smooth results by interpolating between pairs of input and output values ("stops").
The input may be any numeric expression (e.g., ["get", "population"]). Stop inputs must be numeric
literals in strictly ascending order. The output type must be number, array<number>, or color.

#### Syntax
```
["interpolate",
  interpolation: ["linear"] | ["exponential", base],
  input: number,
  stop_input_1: number, stop_output_1: OutputType,
  stop_input_n: number, stop_output_n: OutputType, ...
]: OutputType (number, array<number>, or Color)
```

### step
Produces discrete, stepped results by evaluating a piecewise-constant function defined by pairs of input and
output values ("stops"). The input may be any numeric expression (e.g., ["get", "population"]).
Stop must be numbers in strictly ascending order. Returns the output value of the stop just less than
the input, or the first output if the input is less than the first stop.

#### Syntax
```
["step",
  input: number,
  stop_output_0: OutputType,
  stop_input_1: number, stop_output_1: OutputType,
  stop_input_n: number, stop_output_n: OutputType, ...
]: OutputType
```
### zoom
Gets the current zoom level. In filter expressions, zoom expression evaluates to integer values only(for
rendering, appropriate value is chosen by rounding current fractional zoom to the nearest integer).

#### Syntax
```
["zoom"]: number
```

### heatmap-density
Gets the kernel density estimation of a pixel in a heatmap layer, which is a relative measure of how many data points are crowded around a particular pixel. Can only be used in the heatmap-color property.

#### Syntax
```
["heatmap-density"]: number
```

### literal
Provides literal array value.

#### Syntax
```
["literal", [...]]: array
```

### coalesce
Returns first non-null value obtained from expressions in list.

#### Syntax
```
["coalesce", OutputType, OutputType, ...]: OutputType
```

### type-asserting expressions
Ensures that incoming value has specified type. Aborts whole expression if types differ.

```
["number", value]: number

["number", value, fallback: value, fallback: value, ...]: number

["string", value]: string

["string", value, fallback: value, fallback: value, ...]: string

["boolean", value]: boolean

["boolean", value, fallback: value, fallback: value, ...]: boolean

["array", type: "string" | "number", value]: array<type>

["array",
    type: "number" | "string",
    N: number (literal),
    value
]: array<type, N>
```

## On name templates in library references

Library image reference may contain a name template. Name templates provide a way to bind icon in library to a specific attribute. Consider an example:
Feature has attrbute 'icon' which can be either 'shop' or 'monument'. By using following name template one can create a single style suitable for all features:

`poi_{icon}`

Name templates also enable complex chains of icon fallbacks. If 'icon' is an array ['grocery', 'shop'], client renderer will try to use icons in the following order:
poi_grocery, poi_shop.

In some cases there might be different versions of icon and we may want try them in particular order. This can be done by using following syntax:

`poi_{icon}_(30|20)`

Using feature from previous example, this will result into following ordered list of possible icon names: `['poi_grocery_30', 'poi_grocery_20', 'poi_shop_30', 'poi_shop_20']`.

Nested curly/round brackets are not supported, `'({icon}|20|30)'` will result in `['{icon}', '20', '30']`.

