---
slug: step6
id: mgsgris6xyae
type: challenge
title: Enable Application Ingress
notes:
- type: text
  contents: |-
    In the last learning module, we cover Application Ingress with ACS and the following Concepts:

    * Create an example Wordpress Application using GitOps and ACS
    * Ensure there is a matching Prod PlacementRule
    * Enable Cluster Ingress
    * Review both managed Clusters
    * Finally, test the Ingress for both Wordpress sites on both Clusters

    Let's begin!
tabs:
- title: Terminal 1
  type: terminal
  hostname: container
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: Spoke1 Wordpress
  type: service
  hostname: spoke1
  path: /
  port: 31500
- title: Spoke2 Wordpress
  type: service
  hostname: spoke2
  path: /
  port: 31500
- title: ACS Hub Console
  type: website
  url: https://multicloud-console.crc-lgph7-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: advanced
timelimit: 6000
---
Login to the ACS Console

![perspective-toggle](../assets/acs-login-console.png)

Completed, move onto the next assignment.