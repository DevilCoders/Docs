To add a new formula
--------------------
1. Place your _*.info_ file here (_extsearch/geo/meta/rearrs/mxnet_formulas_ directory).
2. Add its name to the `LARGE_FILES` list in _ya.make_.
3. Launch `ya upload --update-external` (filename is not specified: the uploader recognizes new files automatically). This command uploads files to Sandbox and creates small JSON-based _*.external_ files which hold only metadata.
4. Add the newly created _*.external_ file to your VCS and commit it together with changes in _ya.make_.

To deploy
---------
1. After commit, navigate to [the New CI][1].
2. Click on the latest release and wait the build to complete.
3. Open the corresponding `KOSHER_YA_MAKE` Sandbox task.
4. Release the task:
   * Choose **testing** to deploy to `addrs_upper_r1` automatically.
   * Choose **stable** to deploy to `addrs_upper`.

![open task](https://jing.yandex-team.ru/files/sobols/browser_cAPKwB2tx0.png)

![release task](https://jing.yandex-team.ru/files/sobols/browser_Bgcntyn9PK.png)

To build formulas without commit
--------------------------------
Perform the steps listed above to add a formula.
Create a new review (pull request). A build task on Sandbox will be launched automatically.
Click on "Build formulas flow" merge check to find this task and possibly release it.

![card](https://jing.yandex-team.ru/files/sobols/browser_sHzdMFKHQJ.png)

[1]: https://a.yandex-team.ru/projects/geosearch2/ci/releases/timeline?dir=extsearch%2Fgeo%2Fmeta%2Frearrs%2Fmxnet_formulas&id=formulas-release
