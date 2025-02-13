To manage a mix of On-Demand and Spot Instances across multiple instance types within an Auto Scaling group (ASG), AWS requires a launch template. Here’s why:

* Launch Templates Support Mixed Instance Policies

1. A launch template is required when using multiple instance types in an Auto Scaling group.
2. You cannot use a launch configuration for mixed instance types because launch configurations support only a single instance type.
3. Auto Scaling with Mixed Instances Requires Launch Templates

AWS Auto Scaling groups support MixedInstancesPolicy, which allows the combination of On-Demand and Spot Instances.
The MixedInstancesPolicy requires a launch template, not a launch configuration.
Flexibility and Cost Optimization

By defining a MixedInstancesPolicy in the Auto Scaling group, AWS can:
Use On-Demand Instances for baseline capacity.
1. Use Spot Instances to reduce costs while maintaining availability.
2. Distribute workloads across multiple instance types.
3. Instance Distribution and Allocation Strategy

A launch template allows customizing instance types, weights, and allocation strategies (e.g., lowest price, capacity-optimized). The Auto Scaling group can dynamically adjust capacity based on demand.
Key Takeaway
1. Launch templates are mandatory when provisioning multiple instance types in an Auto Scaling group.
2. They allow defining a MixedInstancesPolicy to combine On-Demand and Spot Instances efficiently.
3. Launch configurations do not support MixedInstancesPolicy, making launch templates the only option.
