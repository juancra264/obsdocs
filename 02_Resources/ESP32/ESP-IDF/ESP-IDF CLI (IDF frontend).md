## Export to use idf.py command:

To enable the `idf.py` CLI and its autocompletion features, you must **source the export script** for your specific operating system:

- **Linux/macOS**: Run
```bash
$HOME/esp/esp-idf/export.sh
``` 

- **Windows (PowerShell)**: Run `. 
```powershell
$HOME/esp/esp-idf/export.ps1
```
## Create a project

```bash
idf.py create-project <name>
```

## Configuration

Set ESP module (esp32, esp32s3, esp32c3)

```
idf.py set-target <target>
```

 Open TUI for SDK configuration
 
```
 idf.py menuconfig   
```

Add dependency or component:
```
idf.py add-dependency "espressif/led_strip^3.0.3"
```

## Build and Flash

Compiles the project
```
idf.py build
```

Flashes the firmware
```
idf.py -p <PORT> -b <BAUD> flash
```

Opens serial monitor
```
idf.py -p <PORT> monitor
```

Combines flashing and monitoring
```
idf.py -p <PORT> flash monitor
```


## Additional Commands

- **`idf.py clean`**: Removes build output files but keeps configuration. 
    
- **`idf.py fullclean`**: Deletes the entire build directory and CMake cache. 
    
- **`idf.py size`**: Displays firmware size information (RAM/Flash usage).  
    
- **`idf.py docs`**: Opens the relevant documentation in a browser.