
# Azure Resource Tagging Strategy

## Purpose of Tagging
Tagging resources in Azure helps in organizing, managing, and tracking cloud costs efficiently. 
The following tags are applied to all deployed resources to improve governance and cost analysis.

## Tagging Strategy

| Tag Key       | Tag Value | Purpose |
|--------------|-----------|------------------------------------------------------------|
| Environment  | Test      | Identifies the resource as part of a testing environment |
| Department   | IT        | Associates the resource with the IT department for cost tracking |

![Image](https://github.com/user-attachments/assets/a0d983a2-d473-4986-9c47-96e10d35ec02)

## Best Practices
- Ensure all resources have the **Environment** and **Department** tags.
- Use consistent and standardized tag names across all resources.
- Apply these tags during resource deployment to maintain uniformity.

## Summary
Tagging resources in Azure improves visibility and cost allocation. 
By using **Environment: Test** and **Department: IT**, we ensure proper categorization and tracking.

