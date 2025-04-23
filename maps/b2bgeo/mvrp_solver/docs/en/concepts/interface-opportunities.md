# Planning routes through the interface

To start planning, go to the Yandex.Routing website and do the following:

1. Follow the [https://yandex.com.tr/courier/](https://yandex.com.tr/courier/) link and log in **using the email address that you specified when signing up**.
2. Click the **Planning** menu on the left of the screen.

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step2_en.png"/>

3. Click **Start planning**:

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step3_en.png"/>

4. Select the **Fast** solution quality (trial optimization) and click **Start planning**.
  Note that planning with the Low quality doesn't guarantee high-quality optimization. To get reliable results, use Normal or High modes.

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step4_en.png"/>

5. Upload the vehicle and order settings from the sample that you [downloaded earlier](example.md).

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step5_en.png"/>

6. Make sure that all the vehicle and order settings are uploaded correctly.  A demo of the planning that you're working with at the moment is always uploaded correctly.

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step6_en.png"/>

7. Click **Solve** and wait for the optimization to complete.

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step7_en.png"/>

8. Optimized routes will be displayed on the map and in a table named **Routes**.

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step8_en.png"/>

9. You can also download the routes in Excel format:

  <img class="step--img" src="https://courier.yandex.ru/vrs-doc/step9_en.png"/>

{% note %}
**Congratulations!**

You've performed your first route optimization. You can now move on to defining business requirements,
creating your own requests, and [evaluating the economic efficiency of using Yandex.Routing](economic-effect.md).

To get advice on any issues, contact your Yandex.Routing account manager.
{% endnote %}

## Editing a solution

After a planning task is completed, you can work with the results using the API or through the planning interface. In the planning interface, you can:

- View the main metrics of planning results.
- View the created routes on the map.
- See how orders are distributed across the routes.
- Edit the routes and see how the solution metrics change.

To start working with the available planning result via the web interface, follow the link:

`https://yandex.com.tr/courier/companies/<company_id>/depots/all/mvrp/<task_id>`

where:

- `company_id` is your company ID.
- `task_id` is the solution ID received in the response to the perform planning task request.

If you don't have access to the planning interface or you can't find your company_id, contact your account manager.

In the interface that opens, you can see all planned routes.

- In the Routes table, you can see the route metrics and final metrics of the solution.

- In the Undistributed Orders table, you can see orders that failed to be included in the routes due to the specified restrictions:
<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_ui_en.png"/>

Click on a route on the map or in the Routes table to open the Orders window with detailed information.

Route editing features:

- To remove an order from delivery routes, drag the order row to the Undistributed Orders table in the Orders window. Or vice versa: you can transfer an order from Undistributed ones to a route or a vacant vehicle. To work with multiple items, press and hold the Ctrl key and select multiple items.

- To move an order from one route to another, drag the order row from the Orders table to the Routes table on the target route row, or drag the order point on the map to another route line.

Currently, you can't edit the sequence of delivery to points.

When editing routes, the system automatically recalculates the totals of the built routes. If they're changed in the Routes table, the indicators that have improved or worsened are accompanied by green or red icons that indicate the difference between the edited routes and the original planning results.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_routes_en.png"/>

The system handles each edit as a separate task. So every time you make a change to the planning, a new link is generated (it's available in the browser address bar). If you want to save the edited results so that you can resume working with the routes, just save the resulting link. The solution and results from the source link do not change when editing.

## Saving the final solution

If you have finished editing and want to download the final solution, click Export in the planning interface. Then, you can download the results in Excel or JSON format.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_export_button_en.png" width="310px" />

To upload the planning results to your system using a link to the results in JSON format, click Export -> Export to JSON. In the export window, you'll see a link to the solution that you can copy.

You can't edit the final solution obtained this way.

<img class="step--img" src="https://courier.yandex.ru/vrs-doc/step1_export_en.png" width="310px" />

<p class="p"><a href="feedback.html" class="xref button">Write to Support</a></p>
