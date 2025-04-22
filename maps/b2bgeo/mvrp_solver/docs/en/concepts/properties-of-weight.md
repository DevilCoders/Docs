# Weight and volume properties

In a request to the Router, you can set the vehicle load capacity and the weight of orders.

Two measurement systems are supported:

- Actual weight in kilograms and volume weight.
- Unit weight (pallets, boxes, or kegs).

## Actual and volume weight

In the Router, you can set the order weight or the vehicle load capacity in kilograms and the order volume and the vehicle capacity in cubic meters.

The weight and volume are related measures:

- If the weight is specified and the volume is not, the volume is calculated automatically based on the equation 250 kg = 1 m³.
- If the volume is specified and the weight is not, the weight is calculated automatically using the same equation.
- If both the weight and volume are specified, automatic calculation is not performed and custom values are used.

## Unit weight

In addition to weight and volume units specified in the metric system, the Router enables you to set the order size and the vehicle capacity in abstract weight units.

An abstract weight unit is usually a whole and indivisible object (for example, a pallet, a box, or a keg). However, sometimes, instead of cargo units (such as pallets), you need to use some conventional units of measurement: most often when there are shipment specifics for different categories of product items.

For example, pallet stacking is allowed for one product and not allowed for another product. In this case, the vehicle capacity for these products, measured in pallets, will be different. Then, at the stage of preparing the input data, you need to calculate certain adjusted capacity values as units (in this case, the Router supports fractional unit values).

For example, there is a vehicle with a capacity of 12 pallets, but product 1 can be loaded in the amount of 15 pallets (due to stacking) and all other products require exactly 12 pallets. In this case, 1 pallet of product 1 must be converted into 0.8 regular pallets when transmitting data to the Router.

{% note %}

Please note that the unit weight or volume is considered regardless of the specified order weight and volume or vehicle capacity. For example, the load capacity of a vehicle may be limited to 20 tons or 10 pallets and the vehicle will be considered fully loaded when one of the weight measurements is reached.

{% endnote %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

