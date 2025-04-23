##Sandbox LXC Image for CatBoost performance tests.

Allows to build CatBoost python package wheels in open source configurations and run performance tests.

Includes all supported versions of python (2.7, 3.5, 3.6, 3.7) with dependencies for CatBoost, run_python_package_train and LightGBM and XGBoost.

###How to create image.

Use ``SANDBOX_LXC_IMAGE`` sandbox task.

Non-default task parameters to set:

* ``ubuntu_release`` - ``xenial``
* ``Create custom LXC image`` - enable this flag.
* ``Additional package repositories`` - Yandex Ubuntu Xenial repositories can be added here. See example task for actual contents.
* ``Shell script to execute during final stage``. Copy the contents of ``install.sh`` file in this directory to this form field.

[Example task](https://sandbox.yandex-team.ru/task/514202281/view)
 