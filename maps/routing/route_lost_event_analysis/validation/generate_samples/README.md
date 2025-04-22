Generate samples from a given class of route lost events
=========================

A tool to assess the quality of classes produced by route lost event classifier

How to run
----------

0. Make sure you have access to the `sample` and `summary` tables produced by [classifier](../../classifier) or simply use the outputs of [this sandbox task](https://sandbox.yandex-team.ru/scheduler/22340).

1. Run [visualization tool](../../visualize_data) in a separate session with the same road graph version used for classification.

2. Run `generate_samples` tool passing `sample` and `summary` tables as well as the url to the visualizer as inputs.

3. The tool will print some urls for the selected route lost events to stdout. You may want to redirect this output to a file for convenience. Please use these links to carefully assess the quality of the samples following [this guide](https://wiki.yandex-team.ru/maps/dev/core/routing/Guide-for-route-lost-event-classifier-quality-assessment/).
