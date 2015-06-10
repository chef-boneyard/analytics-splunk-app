# Chef Analytics Splunk App

Splunk App to gather insights from your Chef infrastructure via Chef Analytics.

## Requirements:

* Chef Analytics 1.1.4 or later

## Screenshots:

### Nodes Activity Dashboard
![Nodes Activity Dashboard](./appserver/static/nodes-graphs.png)

### Server Activity Dashboard
![Server Activity Dashboard](./appserver/static/server-activity.png)

## Setup:

1. [Download](https://downloads.chef.io/analytics/) and [install](https://docs.chef.io/install_analytics.html) Chef Analytics.
2. Configure a notification for your Splunk Server:
  * Go to `Notifications` tab in your Analytics UI.
  * Click `+` and select `Splunk`.
  * Give your configuration a name for e.g. `my-splunk-notifier`
  * Configure `hostname`, `port`, `username` & `password` for your Splunk Server.
  * Port should be `8089`.
3. Create the necessary rules to send data to your Splunk Server. You will need 3 rules:
  ```
  rules 'splunk-actions'
    rule on action
    when
      true
    then
      notify("my-splunk-notifier")
    end
  end
  ```

  ```
  rules 'splunk-actions'
    rule on run_converge
    when
      true
    then
      notify("my-splunk-notifier")
    end
  end
  ```

  ```
  rules 'splunk-run-resources'
    rule on run_resource
    when
      true
    then
      notify("my-splunk-notifier")
    end
  end
  ```

  **NOTE: These rules must be inserted verbatim. Any variance from the rules above will result in a non-functioning integration.

1. Install Chef Analytics Splunk App in your Splunk Server [How do I install a Splunk Packaged App?](http://answers.splunk.com/answers/51894/how-to-install-a-splunk-app.html)

**NOTE: You must be using Splunk Enterprise to be able to install the Chef Analytics for Splunk App. Splunk Light does not support the installation of Packaged Apps.**

[More information on differences between Splunk Enterprise and Splunk light can be found here.](http://www.splunk.com/en_us/products/splunk-light/splunk-light-vs-splunk-enterprise.html)

## Contributing

This project is maintained with [Chef Community Maintenance Policy](https://github.com/chef/chef-rfc/blob/master/rfc030-maintenance-policy.md).

If you have encountered a problem or if you have a feature request, create an issue [here](https://github.com/chef/analytics-splunk-app/issues/new).

[Send in a pull request](https://github.com/chef/analytics-splunk-app/pulls) if you'd like to contribute to this project.

## MAINTAINERS

* Serdar Sutay (serdar at chef dot io)

--------------------------------------------------------------------------------
Copyright:: Copyright (c) 2015 Chef Software, Inc.
License:: Apache License, Version 2.0

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
