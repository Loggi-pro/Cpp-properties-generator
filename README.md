# C_CPP_PROPERTIES Generator

Generate c_cpp_properties.json file for VSCode based on template.

# Usage

**--file=**\<path to c_cpp_properties.json file\>  
**--name=**\<name of config\> *optional (`Generated config` by default)  
**-f**\<force include file\>  
**-i**\<include directory\>  
**-D**\<compile defines\>  
**-cc**\<path to compile_commands.json\> *optional

Command will create config with specified `name`, or overwrite it, if i's not exists.

## Example

```
python gen-cpp-properties.py --file=.vscode/c_cpp_properties.json --name="Config file" -fC:/lib/avr/include/avr/io.h -fC:/lib/void/platform_specific.h -DMCU=atmega168p -DF_CPU=16000000UL -iC:/lib/avr/include -cc=build/compile_commands.json
```

## Result

```json
{
	"configurations": [
		{
			"name": "Config file",
			"cStandard": "c99",
			"cppStandard": "c++17",
			"intelliSenseMode": "gcc-x64",
			"includePath": ["C:/lib/avr/include"],
			"defines": ["MCU=atmega168p", "F_CPU=16000000UL"],
			"forcedInclude": ["C:/lib/avr/include/avr/io.h", "C:/lib/void/platform_specific.h"],
			"compileCommands": "build/compile_commands.json"
		}
	]
}
```

## From CMake

```cmake
execute_process(
    COMMAND ${PYTHON_EXECUTABLE} ${CURRENT_DIR}/gen-cpp-properties.py
        "--file=${CPPTOOLSFILE_PATH}"
        ${force_include_list_path}
        ${compile_defines}
        ${include_dirs}
        "-cc=${COMPILE_COMMANDS}"
	WORKING_DIRECTORY ${CURRENT_DIR}
	RESULT_VARIABLE rv
)
```

# Tuning

Other config parameters can be changed by editing `jsonTemplate` variable in `.py` file.
