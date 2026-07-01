# HashiCorp Certified Terraform Associate (004) Technical Study Guide

## 1. Introduction to Infrastructure as Code (IaC)

### Defining Infrastructure as Code

Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. It allows operators to treat infrastructure with the same rigor as application code.

### Key Advantages of IaC

- **Version Control:** Configurations act as the source of truth and can be stored in Git to track changes, audit history, and enable rollbacks.
- **Automation:** Speeds up deployment cycles by removing manual provisioning bottlenecks.
- **Consistency:** Eliminates snowflake servers and environment drift by ensuring development, staging, and production environments are identical.
- **Repeatability:** Enables the reliable recreation of entire infrastructure stacks in minutes.
- **Risk Reduction:** Minimizes human error associated with manual GUI configurations and terminal commands.

### Terraform’s Multi-Cloud Role

Terraform is a service-agnostic tool that manages multi-cloud, hybrid, and on-premises workflows. Unlike provider-specific tools such as CloudFormation, Terraform uses a unified HCL (HashiCorp Configuration Language) to interact with diverse APIs, allowing a single workflow to manage resources across AWS, Azure, GCP, and private data centers.

---

## 2. Terraform Fundamentals

### Providers and Plugins

Providers are executable binaries that act as the interface between Terraform and a specific service API.

- **Installation:** Providers are downloaded automatically during `terraform init`.
- **Versioning:** Use the `required_providers` block inside the `terraform` block to pin specific versions, preventing breaking changes when new provider versions are released.

### The Dependency Lock File and Upgrades

The `.terraform.lock.hcl` file is generated during `terraform init`. It ensures that every team member uses the exact same provider version and checksum.

- **Exam Trap:** Modifying a version constraint in your HCL is not enough to update the lock file. You must run `terraform init -upgrade` to update the lock file to the newest allowed version.

| Feature | `terraform.tfstate` | `.terraform.lock.hcl` |
|---|---|---|
| Primary Focus | Infrastructure reality | Dependency consistency |
| Content | Resource IDs, metadata, and current status | Provider versions and security checksums |
| Source of Truth | Maps configuration to real-world objects | Ensures all environments use the same plugins |

---

## 3. The Core Terraform Workflow

### Step-by-Step Command Analysis

- `terraform init`: Prepares the working directory. It downloads providers and modules, initializes the backend, and creates the hidden `.terraform/` directory.
  - **Migration nuance:** When changing backends, use `-migrate-state` to attempt to copy existing state to the new location, or `-reconfigure` to ignore existing state and start fresh.
- `terraform validate`: A local-only check for syntax and internal consistency. It does not verify credentials or cloud-side resource availability.
- `terraform plan`: Generates an execution plan by comparing state to the configuration. It refreshes the state and tests credentials by reading infrastructure, but makes no changes.
- `terraform apply`: Executes the plan to reach the desired state. It updates the state file upon success.
- `terraform destroy`: Removes all infrastructure managed by the current configuration.

### Formatting

`terraform fmt` standardizes HCL files to the canonical format (indentation and spacing). It is essential for team collaboration to ensure code remains readable and diff-friendly.

---

## 4. Terraform Configuration Language (HCL)

### Resource and Data Blocks

- **Resource blocks:** Declare components Terraform manages (for example, an EC2 instance).
- **Data blocks:** Perform read-only queries to fetch information from existing infrastructure (for example, finding the latest Ubuntu AMI ID).

### Complex Types: Collections vs. Structural

Understanding how Terraform groups data is critical for the exam:

1. **Collection types** (homogeneous): All elements must be the same type.
   - `list`: Ordered sequence.
   - `map`: Key-value pairs.
   - `set`: Unordered collection of unique values.
2. **Structural types** (heterogeneous): Can contain multiple types.
   - `object`: Named attributes with specific types.
   - `tuple`: Fixed-length sequence of specific types.

### Resource Addressing and Dependencies

| Dependency Type | Definition | Example |
|---|---|---|
| Implicit | Created when one resource references an attribute of another | `${aws_instance.web.id}` |
| Explicit | Manually defined when Terraform cannot see a hidden link | `depends_on = [...]` |

---

## 5. Advanced Validation and Version 004 Features

### Ephemeral Values (New in 004)

Ephemeral values and write-only arguments are security-centric features. They allow Terraform to handle sensitive data required for a provider (such as a temporary token) without ever writing that value to the `terraform.tfstate` file. This reduces the risk of sensitive data exposure in your state storage.

### Custom Validation Conditions

Use `validation` blocks within input variables to enforce guardrails on user-provided values.

```hcl
variable "instance_size" {
  type = string

  validation {
    condition     = contains(["t2.micro", "t3.small"], var.instance_size)
    error_message = "The instance size must be either t2.micro or t3.small."
  }
}
```

### Check Blocks and Lifecycle Rules

- `check` blocks: Perform post-apply validation to ensure the continued health of infrastructure (for example, checking if a website returns `200 OK`) without causing the deployment itself to fail.
- Lifecycle rules: The `create_before_destroy` argument modifies the default behavior to ensure a new resource is running before the old one is terminated, minimizing downtime.

### Moved and Removed Blocks

- `moved`: Refactor code (for example, moving a resource into a module) without triggering a destroy/recreate cycle.
- `removed`: Removes a resource from Terraform state management without deleting the actual physical resource in the cloud.

---

## 6. Terraform State Management

### Backends and Locking

- **Local backend:** Stores state in a local `terraform.tfstate` file.
- **Remote backend:** Highly recommended for teams (S3, GCS, HCP Terraform). It centralizes state and enables state locking, preventing concurrent writes from corrupting state.

### Refresh-Only Mode

Running `terraform apply -refresh-only` updates the state file to match the current real-world state of the infrastructure. It does not modify cloud resources; it only reconciles the state file with drift that occurred outside Terraform.

### State CLI Operations

- `terraform state list`: Lists resources in the state.
- `terraform state show <address>`: Displays detailed attributes for one resource.
- `terraform state rm <address>`: Stops Terraform from managing a resource. Note: The resource remains in the cloud.

---

## 7. Module Composition

Modules are containers for multiple resources. Every configuration has a root module that can call child modules.

- **Scope:** Variables are scoped to the module. To use a value from a child module in the root module, the child module must define an output.
- **Versioning:** Always use the `version` argument when sourcing from a registry to ensure stability against upstream module changes.

---

## 8. HCP Terraform (Cloud) & Governance

HCP Terraform is a managed SaaS platform, while Terraform Enterprise is the self-hosted, on-premises equivalent.

- **Workspaces:** Persistent environments that store state, variables, and run history.
- **Variable Sets:** Allows applying the same group of variables across multiple workspaces.
- **Run Triggers:** Link workspaces so that a successful apply in one workspace triggers a plan in another.
- **Governance:** Sentinel and OPA enforce policy-as-code between plan and apply.

---

## 9. Maintenance, Security, and Troubleshooting

### Infrastructure Import

The `terraform import` command brings existing resources into state.

- **Trap:** `import` only updates the state file. It does not generate HCL code. If you run `terraform apply` immediately after an import without writing the HCL code, Terraform may attempt to destroy the resource because it is not defined in the configuration.

### Sensitive Data

The `sensitive = true` parameter masks values in CLI output and logs but does not encrypt the value in the plain-text state file. Use encrypted backends or Vault for true secret management.

### Verbose Logging

Set `TF_LOG` to one of five levels: `TRACE`, `DEBUG`, `INFO`, `WARN`, or `ERROR`. Use `TF_LOG_PATH` to save logs to a file.

---

## 10. Exam Preparation Summary

### Quick-Reference Command Table

| Command | Primary Function | Reads State | Writes State | Real-World Impact |
|---|---|---|---|---|
| `init` | Initialize directory | No | No | None |
| `validate` | Check configuration syntax | No | No | Detects local errors |
| `plan` | Preview changes | Yes | No | Shows proposed changes |
| `apply` | Deploy changes | Yes | Yes | Creates/updates/deletes resources |
| `destroy` | Remove resources | Yes | Yes | Deletes resources |
| `refresh` | Sync state with reality | Yes | Yes | Adjusts state only |
| `import` | Add existing resource to state | No | Yes | Maps existing resources |

---

## 11. Practice Questions

### Q1: Provider lock file update
**Question:** You modified a provider version constraint in your HCL. Which command and flag must you run to update the dependency lock file?

**Answer:** `terraform init -upgrade`

**Rationale:** A standard `terraform init` won't change the lock file if it is already present. The `-upgrade` flag is required to recalculate the lock file checksums.

### Q2: Import without HCL
**Question:** What happens if you run `terraform apply` after importing a resource without adding the HCL code?

**Answer:** Terraform will attempt to destroy the resource.

**Rationale:** Terraform ensures reality matches configuration. If the configuration does not declare the imported resource, Terraform may delete it to reconcile state and code.

### Q3: Central variable management in HCP Terraform
**Question:** Which HCP Terraform feature allows you to manage variables for dozens of workspaces in one central place?

**Answer:** Variable Sets.

**Rationale:** Variable Sets allow for global application of variables across a group of workspaces or an entire organization.

### Q4: HCP Terraform vs Terraform Enterprise
**Question:** Distinguish between HCP Terraform and Terraform Enterprise.

**Answer:** HCP Terraform is SaaS hosted by HashiCorp; Terraform Enterprise is self-hosted on-premises.

**Rationale:** This is a core 004 objective focusing on delivery model differences.

---

## 12. Watch Outs

- `terraform state rm` vs `terraform destroy`: `state rm` removes the resource from state; `destroy` deletes the resource in the cloud.
- Ephemeral values: Prevent sensitive data from reaching the state file.
- Lock file vs state file: Lock = providers; state = resources.
- `terraform fmt`: Standardizes formatting, even if the code is logically broken.

fmt / validate	Check syntax/style	No	No	None
plan	Preview changes	Yes	No	None
apply	Deploy changes	Yes	Yes	Creates/Updates/Deletes
destroy	Remove resources	Yes	Yes	Deletes resources
refresh	Sync state with reality	Yes	Yes	None
import	Add existing to state	No	Yes	None

Practice Question Logic

Q1: You modified a provider version constraint in your HCL. Which command and flag must you run to update the dependency lock file?

* Answer: terraform init -upgrade.
* Rationale: A standard init won't change the lock file if it's already present. The -upgrade flag is required to recalculate the lock file checksums.

Q2: What happens if you run terraform apply after importing a resource without adding the HCL code?

* Answer: Terraform will attempt to destroy the resource.
* Rationale: Terraform ensures reality matches the configuration. If the configuration is empty, Terraform deletes the resource in reality to match.

Q3: Which HCP Terraform feature allows you to manage variables for dozens of workspaces in one central place?

* Answer: Variable Sets.
* Rationale: Variable Sets allow for global application of variables (like cloud credentials) across a group of workspaces or an entire organization.

Q4: Distinguish between HCP Terraform and Terraform Enterprise.

* Answer: HCP Terraform is SaaS (hosted by HashiCorp); Enterprise is self-hosted (on-premises).
* Rationale: This is a core 004 objective (8b) focusing on delivery model differences.

"Watch Out For" List

* state rm vs destroy: rm deletes the record; destroy deletes the server.
* Ephemeral Values: They prevent sensitive data from reaching the state file.
* Lock File vs State File: Lock = Providers; State = Resources.
* fmt: Always standardizes formatting, even if the code is logically broken.
