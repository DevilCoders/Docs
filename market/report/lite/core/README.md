# TODO
* Ability to use full-weight version of report-data files: categories.xml, etc
* Mock external services: reqwizard, crypta
  cls.index.offers = ...
  cls.reqwizard.expand(text='blabla', syn='bla')
  cls.crypta.user(id='123', gender='male')

* Ideas for mocking crypta and personalization formulas:
  - in universal config there will be an ability to write in-place formulas on json and refer to it
  - in tests invent good way of formula presentation, then translate it to config
  - crypta mock, which returns predefined values on predefined input

* Quick updates test:
  - on tear down MUST be reverted
    self.update.qbids(...)
    self.update.qindex(...)

    self.report.request_xml('admin_action=qbids')
    self.report.request_xml('admin_action=qindex').assert_ok()
    
* Support click url extraction from bsformat
* Better diag in log assertions
* Use ya tool python
* Logical link from data in index to test case (on error -- print data)

