# Sample planning

Let's take a look at an example of route planning that uses [basic settings](quickstart.md):

- A company has 56 vehicles with a load capacity ranging from 1000 kg to 3400 kg.
- All vehicles start their route at the depot.
- A vehicle shift is considered finished after the last order is completed. The vehicles don't return to the depot at the end of the working day.
- The depot operating hours are from 08:00 to 22:00.
- During the next day, 150 orders of different weight and volume should be delivered at different locations.
- Geocoding of depot and order delivery addresses (their conversion to geographical coordinates) is done.

Sample optimization request sent through the API in JSON format:

- **[Download a sample request in JSON format](https://courier.yandex.ru/vrs/api/v1/log/request/618dfd6e-dcaf6824-b5bb4908-974fa72c)**

Sample optimization request made via the logistician dashboard in Excel format:

- **[Download a simplified sample request in Excel format](https://courier.yandex.ru/vrs-doc/mvrp-example-easy.xlsx)** (only contains the parameters required for optimization)

- **[Download a complete sample request in Excel format](https://courier-admin.s3.yandex.net/mvrp-example.xlsx)** (with all possible request parameters)

{% note %}

You can find our comments and pre-configured vehicles, orders, and depot on the corresponding sheets. The column headers in the file are filled with color depending on the parameter significance:

- Red indicates required or highly recommended parameters for all requests.
- Yellow indicates optional parameters that are important for optimization.
- Black indicates parameters that are used to fine-tune the order delivery model.
- Gray indicates parameters for advanced users. Using these parameters, one can fine-tune planning tasks.

{% endnote %}

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>

