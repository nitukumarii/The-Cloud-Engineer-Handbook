### Blue-Green vs Canary deployment 


# Blue-Green vs Canary Deployment

In Blue-Green deployment, we maintain two identical environments. The existing production environment runs the old version (Blue), and we deploy the new version to the second environment (Green). We test and validate the new environment, 
monitor application health and alerts, and once everything is stable, we switch traffic from the old environment to the new environment. 
If any issue occurs, we can quickly switch traffic back.

In Canary deployment, we deploy the new application version to a small set of pods or instances while the existing version continues 
serving traffic. We monitor key metrics like error rate, latency, and application health. If the canary version is stable, 
we gradually replace the old pods with new pods until the complete application runs on the new version.
