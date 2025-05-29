# Neuropsych Domain Template Functions Guide

## Overview

This guide explains how to use the newly created R functions that simplify the creation and management of neuropsychological domain templates in your reports. The solution replaces the redundant code in your domain-specific `.qmd` files with reusable functions.

## Key Components

1. **domain_template.R**: Core module with reusable functions
2. **example_usage.R**: Examples of how to use the functions

## Benefits

- **Reduced redundancy**: No more copying large chunks of code between domain files
- **Improved maintainability**: Changes to the template structure only need to be made in one place
- **Simplified workflow**: Create new domain files with minimal configuration
- **Consistent structure**: All domain files follow the same pattern

## Using the Functions

### Basic Usage

To create a domain-specific Quarto document:

```r
source("domain_template.R")

# Define domain information
executive_domain <- list(
  domain = "Attention/Executive",
  pheno = "executive"
)

# Run the workflow (creates and renders the file)
run_neuropsych_domain(executive_domain)
```

### Customization Options

You can customize various aspects of the domain:

```r
memory_domain <- list(
  domain = "Memory",
  pheno = "memory",
  
  # Custom scales (if not provided, uses defaults for the domain)
  scales = c("Scale1", "Scale2", "Scale3"),
  
  # Custom plot titles
  subdomain_plot_title = "Memory functions are crucial for cognitive processing.",
  narrow_plot_title = "Memory performance across narrow abilities.",
  
  # Specific scales to exclude from plots
  exclude_from_plots = c("Memory Index", "Working Memory Index"),
  
  # Additional filtering for tables
  table_filters = c(
    "dplyr::filter(test_name != 'CVLT-3 Brief')",
    "dplyr::filter(scale != 'Orientation')"
  ),
  
  # Custom output file (if not provided, uses standard naming convention)
  output_file = "custom_memory.qmd"
)
```

### Processing Multiple Domains

You can process multiple domains in a batch:

```r
domains_to_process <- list(
  executive_domain,
  memory_domain,
  list(domain = "Intelligence", pheno = "iq"),
  list(domain = "Verbal", pheno = "verbal")
)

# Process all domains
lapply(domains_to_process, run_neuropsych_domain)
```

## Function Details

### Main Functions

- `create_neuropsych_domain()`: Creates a domain-specific Quarto document
- `run_neuropsych_domain()`: Creates and renders a domain-specific Quarto document

### Helper Functions

- `generate_qmd_content()`: Generates the Quarto document content
- `get_domain_number()`: Gets the domain number for a given domain
- `get_default_scales()`: Gets default scales for a domain
- `get_domain_groupings()`: Gets test groupings for a domain

## Extending the Functions

To add support for additional domains:

1. Update `get_default_scales()` with domain-specific scales
2. Update `get_domain_groupings()` with domain-specific test groupings

## Example Workflow

1. Source the functions: `source("domain_template.R")`
2. Define your domain configuration
3. Run the workflow: `run_neuropsych_domain(your_domain)`
4. The .qmd file will be created and rendered to Typst

## Next Steps for Further Development

- Add more domain-specific defaults
- Create a full R package
- Add validation for domain parameters
- Create functions to automate common report workflows
