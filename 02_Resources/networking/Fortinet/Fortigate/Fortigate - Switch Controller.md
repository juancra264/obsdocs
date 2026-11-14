# Fortigate - Switch Controller

## Get Mac Address Information

```bash
diag switch-controller switch-info mac-table {{switch-id}} | grep {{port_id}}
```

Example:

```bash
diag switch-controller switch-info mac-table WIMRP-SW-3 | grep port12
```

## Get Port Stats

```bash
diagnose switch-controller switch-info port-stats {{switch-id}} {{port-id}} 
```

Example:

```bash
diagnose switch-controller switch-info port-stats WIMRP-SW-3 port12
```
