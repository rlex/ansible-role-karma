

TeamCity
=========

Ansible role for [karma](https://github.com/prymitive/karma) prometheus alertmanager dashboard.
While this role should work "out-of-the-box", providing you with working karma instance, it's highly recommended to consult [official docs](https://github.com/prymitive/karma/blob/master/docs/CONFIGURATION.md) of karma, since there is alot of stuff which can be customized.  
There is also [example config](https://github.com/prymitive/karma/blob/master/docs/example.yaml) but it doesn't cover all possible settings

## Compatibility
This role is compatible with any modern systemd-based distro.  

## Role Variables
| Variable name                            | Default value        | Description                                |
| ---------------------------------------- | -------------------- | ------------------------------------------ |
| karma_version                            | `0.60`               | version of karma to install                |
| karma_listen_address                     | `0.0.0.0`            | IP to listen on                            |
| karma_listen_port                        | `8512`               | port to listen on                          |
| karma_listen_prefix                      | `/`                  | prefix / folder to listen on               |
| karma_system_user                        | `karma`              | system user for running karma              |
| karma_system_group                       | `karma`              | system group for running karma             |
| karma_karma_name                         | `karma-prod`         | instance name                              |
| karma_alertmanager_interval              | `60s`                | interval for alertmanager query            |
| karma_alertmanager_servers               | default dict         | YAML of alertmanager servers settings      |
| karma_ui                                 | default dict         | YAML of UI settings                        |
| karma_silences_comments_linkdetect_rules | default dict         | YAML of link detect settings               |
| karma_receivers_keep                     | `[]`                 | List of receivers to keep                  |
| karma_receivers_strip                    | `[]`                 | Array of receivers to strip                |
| karma_silenceform_strip_labels           | ` - job`             | Array of labels to strip from silence form |
| karma_grid_sorting                       | default dict         | YAML of grid sorting rules                 |
| karma_filters_default                    | ` - "@state=active"` | Array of default search filters            |
| karma_labels_color_static                | ` - job`             | Array of labels with static colors         |
| karma_labels_color_unique                | ` - cluster`         | Array of labels with unique colors         |
| karma_labels_keep                        | `[]`                 | Array of labels to keep                    |
| karma_labels_strip                       | `[]`                 | Array of labels to strip                   |
| karma_annotations_default_hidden         | `false`              | If true, hide annotations by default       |
| karma_annotations_hidden                 | `[]`                 | Array of annotations to hide               |
| karma_annotations_visible                | `[]`                 | Array of annotations to show               |
| karma_annotations_keep                   | `[]`                 | Array of annotations to keep               |
| karma_annotations_strip                  | `[]`                 | Array of annotations to strip              |

## karma_alertmanager_servers
karma_alertmanager_servers should be written in YAML format as described in [official docs of karma](https://github.com/prymitive/karma/blob/master/docs/CONFIGURATION.md#alertmanagers)
Default setting:
```
karma_alertmanager_servers:
  - name: local
    uri: http://localhost:9093
    timeout: 10s
    proxy: true
    readonly: false
```
Assumes you have karma running on same server as alertmanager and running without any authentication.

## karma_ui
Another setting which is written in YAML as described in [official docs](https://github.com/prymitive/karma/blob/master/docs/CONFIGURATION.md#ui-defaults)

## karma_silences_comments_linkdetect_rules
And another one that follows original YAML format. Write them in format of
```
karma_silences_comments_linkdetect_rules:
  - regex: "(DEVOPS-[0-9]+)"
    uriTemplate: https://jira.example.com/browse/DEVOPS/$1
  - regex: "(DEV-[0-9]+)"
    uriTemplate: https://jira.example.com/browse/DEV/$1
```
    
## karma_grid_sorting 
Last one that follows original YAML as described in [official docs](https://github.com/prymitive/karma/blob/master/docs/CONFIGURATION.md#grid)
There is some default setting:
```
karma_grid_sorting:
  order: label
  reverse: false
  label: severity
  customValues:
    labels:
      severity:
        critical: 1
        warning: 2
        info: 3
```
But depending in your environment and preferences you might need to adjust it for your liking.