## Calling order of AngularJS 1.X functions

- app config
- app run
- directive setup
- directive compile
- (app controller dependencies)
  - service
  - factory
  - inner factory
  - inner service
  - app controller
- filter
- directive linking
- filter render (w.r.t the markup)

## Reference
[What is the calling order of angularjs functions (config/run/controller)?](https://stackoverflow.com/questions/38374145/what-is-the-calling-order-of-angularjs-functions-config-run-controller)
