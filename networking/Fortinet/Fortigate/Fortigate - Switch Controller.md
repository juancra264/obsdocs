# Fortigate - Switch Controller

## Get Mac Address Information

```bash
diag switch-controller switch-info mac-table {{switch-id}} | grep {{port_id}}
```

Example:

```bash
diag switch-controller switch-info mac-table WIMRP-SW-3 | grep port12
```
