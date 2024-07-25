# STM32 + Visual Studio Code + Make + Windows Tutorial

This is a tutorial / guide / template project to configure a custom IDE for STM32 microcontrollers. STM32F103C8T6 microcontroller is used as an example.

## Installation

### 1. Arm GNU Toolchain.

Follow this [link][Arm GNU Toolchain]. Navigate to "Downloads" -> "Windows (mingw-w64-i686) hosted cross toolchains" -> "AArch32 bare-metal target (arm-none-eabi)" -> "arm-gnu-toolchain-13.3.rel1-mingw-w64-i686-arm-none-eabi.zip". Download the archive.

![1_Arm_GNU_Toolchain_text][1_Arm_GNU_Toolchain]

Unpack the archive. Add "bin" to the system PATH environment variable.

![2_Arm_GNU_Toolchain_text][2_Arm_GNU_Toolchain]
![3_Arm_GNU_Toolchain_text][3_Arm_GNU_Toolchain]

### 2. Make from MinGW-w64.

Follow this [link][MinGW-w64]. Navigate to the latest release -> "Assets" -> "w64devkit-1.23.0.zip". Download the archive.

![4_MinGW_w64_text][4_MinGW_w64]

Unpack the archive. Add "bin" to the system PATH environment variable.

![5_MinGW_w64_text][5_MinGW_w64]
![6_MinGW_w64_text][6_MinGW_w64]

### 3. OpenOCD.

Follow this [link][OpenOCD]. Navigate to the latest release -> "Assets" -> "openocd-v0.12.0-i686-w64-mingw32.tar.gz". Download the archive.

![7_OpenOCD_text][7_OpenOCD]

Unpack the archive. Add "bin" to the system PATH environment variable.

![8_OpenOCD_text][8_OpenOCD]
![9_OpenOCD_text][9_OpenOCD]

### 4. STM32CubeMX.

Follow this [link][STM32CubeMX]. Navigate to "STM32CubeMX-Win" -> "Get latest". Download the archive.

![10_STM32CubeMX_text][10_STM32CubeMX]

Unpack the archive. Install STM32CubeMX.

### 5. ST-LINK driver.

Follow this [link][ST-LINK driver]. Navigate to "STSW-LINK009" -> "Get latest". Download the archive.

![11_ST_LINK_driver_text][11_ST_LINK_driver]

Unpack the archive. Install ST-Link driver.

### 6. System View Description.

Go to the official web page of your STM32 microcontroller. Navigate to "CAD Resources" -> "All resources" -> "System View Description". For STM32F103C8T6 follow this [link][System View Description]. Navigate to "STM32F1 System View Description". Download the archive.

![12_System_View_Description_text][12_System_View_Description]

Unpack the archive. Navigate to "STM32F1_svd_V1.2" and select "STM32F103.svd" file.

![13_System_View_Description_text][13_System_View_Description]

Copy "STM32F103.svd" file into your project folder.

![14_System_View_Description_text][14_System_View_Description]

### 7. Visual Studio Code.

Follow this [link][VSCode]. Navigate to "Download for Windows". Download the installer.

![15_Visual_Studio_Code_text][15_Visual_Studio_Code]

Install Visual Studio Code.

### 8. "C/C++" VSCode extension.

Follow this [link][C/C++ VSCode extension]. Or open VSCode, navigate to "Extensions", type "C/C++" into the search bar and click "Install".

![16_C_VSCode_extension_text][16_C_VSCode_extension]

### 9. "Makefile Tools" VSCode extension.

Follow this [link][Makefile Tools VSCode extensions]. Or open VSCode, navigate to "Extensions", type "Makefile Tools" into the search bar and click "Install".

![17_Makefile_Tools_VSCode_extension_text][17_Makefile_Tools_VSCode_extension]

### 10. "Cortex-Debug" VSCode extension.

Follow this [link][Cortex-Debug]. Or open VSCode, navigate to "Extensions", type "Cortex-Debug" into the search bar and click "Install".

![18_Cortex_Debug_VSCode_extension_text][18_Cortex_Debug_VSCode_extension]

### 11. "Todo Tree" VSCode extension.

Follow this [link][Todo Tree]. Or open VSCode, navigate to "Extensions", type "Todo Tree" into the search bar and click "Install".

![19_Todo_Tree_VSCode_extension_text][19_Todo_Tree_VSCode_extension]

### 12. "Doxygen Documentation Generator" VSCode extension.

Follow this [link][Doxygen Documentation Generator]. Or open VSCode, navigate to "Extensions", type "Doxygen Documentation Generator" into the search bar and click "Install".

![20_Doxygen_Documentation_Generator_VSCode_extension_text][20_Doxygen_Documentation_Generator_VSCode_extension]

## Configuration

### 1. Generate initialization source code with STM32CubeMX.

Open ST32CubeMX.

![21_Generate_code_text][21_Generate_code]

Navigate to "File" -> "New Project …".

![22_Generate_code_text][22_Generate_code]

Select your STM32 microcontroller. Navigate to "Commercial Part Number" and type "STM32F103C8T6". Navigate to "MCUs/MPUs List" -> "STM32F103C8T6". Click "Start Project".

![23_Generate_code_text][23_Generate_code]

Enable Serial Wire Debug interface. Navigate to "Pinout & Configuration" -> "Categories" -> "System Core" -> "Sys" -> "SYS Mode and Configuration" -> "Mode" -> "Debug" and select "Serial Wire".

![24_Generate_code_text][24_Generate_code]

Configure specific general-purpose input/output port as output push-pull to drive an LED. On my development board pin PC13 is connected to an LED. Click on pin PC13 and select "GPIO_Output".

![25_Generate_code_text][25_Generate_code]

Navigate to "Pinout & Configuration" -> "Categories" -> "System Core" -> "GPIO" -> "GPIO Mode and Configuration" -> "Configuration" -> "GPIO" -> "Pin Name" -> "PC13-TAMPER-RTC" -> "PC13-TAMPER-RTC Configuration" -> "User Label" and enter "LED".

![26_Generate_code_text][26_Generate_code]

Choose your project name. Navigate to "Project Manager" -> "Project" -> "Project Name" and enter "STM32_VSCode_Make_Windows_Tutorial". Navigate to "Project Location" and enter the path, where the new project folder will be created. The result project path is displayed in "Toolchain Folder Location".

Choose your IDE / build tool. Navigate to "Toolchain / IDE" and select "Makefile".

![27_Generate_code_text][27_Generate_code]

Configure code generator settings. Navigate to "Project Manager" -> "Code Generator" -> "STM32Cube MCU packages and embedded software packs" and select "Copy only the necessary library files".

Navigate to "Project Manager" -> "Code Generator" -> "Generated files" and select "Generate peripheral initialization as a pair of '.c/.h' files per peripheral".

![28_Generate_code_text][28_Generate_code]

Click "GENERATE CODE".

![29_Generate_code_text][29_Generate_code]

### 2. Write an LED driver in VSCode.

Open your project folder in VSCode.

![30_Write_LED_driver_text][30_Write_LED_driver]

Create a new folder "App" for your application code. Inside it create a folder "inc" for headers and a folder "src" for source files.

![31_Write_LED_driver_text][31_Write_LED_driver]

Write a header for an LED driver. Create a new file "led.h" inside "App\inc" folder with these contents:

```
#ifndef INC_LED_H_
#define INC_LED_H_


void led_toggle();


#endif
```

![32_Write_LED_driver_text][32_Write_LED_driver]

Write a source file for an LED driver. Create a new file "led.c" inside "App\src" folder with these contents:

```
#include "main.h"

#include "led.h"


void led_toggle()
{
    HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);
}
```

![33_Write_LED_driver_text][33_Write_LED_driver]

Open "Core\Src\main.c". Include our "led.h" header:

```
/* Includes ------------------------------------------------------------------*/
#include "main.h"
#include "gpio.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include "led.h"
/* USER CODE END Includes */
```

![34_Write_LED_driver_text][34_Write_LED_driver]

Call our `led_toggle` function inside `main` and add a 1 second delay:

```
/* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    led_toggle();
    HAL_Delay(1000);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
```

![35_Write_LED_driver_text][35_Write_LED_driver]

### 3. Configure Make and build tasks.

A default "Makefile" was generated by STM32CubeMX for our project. But now "Makefile" must be modified because custom folders "App\inc" and "App\src" were added to the project.

Open "Makefile" and add "App\inc" folder to C includes:

```
# C includes
C_INCLUDES =  \
-IApp/inc \
-ICore/Inc \
-IDrivers/STM32F1xx_HAL_Driver/Inc \
-IDrivers/STM32F1xx_HAL_Driver/Inc/Legacy \
-IDrivers/CMSIS/Device/ST/STM32F1xx/Include \
-IDrivers/CMSIS/Include
```

![36_Configure_build_tasks_text][36_Configure_build_tasks]

Add all source files in "App\src" folder to C sources:

```
######################################
# source
######################################
# C sources
C_SOURCES =  \
$(wildcard App/src/*.c) \
Core/Src/main.c \
Core/Src/gpio.c \
Core/Src/stm32f1xx_it.c \
Core/Src/stm32f1xx_hal_msp.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_gpio_ex.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_tim.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_tim_ex.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc_ex.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_gpio.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_dma.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_cortex.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_pwr.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_flash.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_flash_ex.c \
Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_exti.c \
Core/Src/system_stm32f1xx.c \
Core/Src/sysmem.c \
Core/Src/syscalls.c  
```

![37_Configure_build_tasks_text][37_Configure_build_tasks]

"Makefile Tools" extension does not output compilation errors to "Problems" panel by default. That's why a separate 
configuration must be created manually.

Create a new folder ".vscode". Inside it create a "settings.json" file with these contents:

```
{
    "makefile.configurations":
    [
        {
            "name": "CustomConfiguration",
            "problemMatchers": ["$gcc"],
        },
    ]
}
```

![38_Configure_build_tasks_text][38_Configure_build_tasks]

Configure VSCode's "Makefile Tools" extension. Navigate to "Makefile" panel -> "MAKEFILE: PROJECT OUTLINE".

Navigate to "Configuration", click on a pencil icon and select "CustomConfiguration".

![39_Configure_build_tasks_text][39_Configure_build_tasks]

Navigate to "Build target", click on a pencil icon and select "all".

![40_Configure_build_tasks_text][40_Configure_build_tasks]

Navigate to "Launch target", click on a pencil icon and select your launch target.

![41_Configure_build_tasks_text][41_Configure_build_tasks]

Inside ".vscode" folder create a "tasks.json" file with these contents:

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks":
    [
        {
            "label": "make build",
            "command": "${command:makefile.buildTarget}",
            "group":
            {
                "kind": "build",
                "isDefault": true
            },
            "options":
            {
                "cwd": "${workspaceFolder}"
            },
        },
        {
            "label": "make rebuild",
            "command": "${command:makefile.buildCleanTarget}",
            "group":
            {
                "kind": "build",
                "isDefault": false
            },
            "options":
            {
                "cwd": "${workspaceFolder}"
            },
        }
    ]
}
```

![42_Configure_build_tasks_text][42_Configure_build_tasks]

Now these build tasks can be called to build our project. Navigate to "View" -> "Command Palette...", type "Tasks: Run Task" and select "make rebuild".

![43_Configure_build_tasks_text][43_Configure_build_tasks]
![44_Configure_build_tasks_text][44_Configure_build_tasks]

Our project is build successfully.

![45_Configure_build_tasks_text][45_Configure_build_tasks]

### 4. Configure VSCode IntelliSense.

VSCode's "C/C++" extension provides real-time IntelliSense. But this extension does not know anything about our toolchain yet. That's why a lot of false errors are displayed in the "Problems" panel.

![46_Configure_IntelliSense_text][46_Configure_IntelliSense]

IntelliSense must be configured to get rid of these false errors. Inside ".vscode" folder create a "c_cpp_properties.json" file with these contents:

```
{
    "configurations": [
        {
            "name": "Cross GCC",
            "includePath": [
                "${workspaceFolder}\\App\\inc",
                "${workspaceFolder}\\Core\\Inc",
                "${workspaceFolder}\\Drivers\\STM32F1xx_HAL_Driver\\Inc",
                "${workspaceFolder}\\Drivers\\STM32F1xx_HAL_Driver\\Inc\\Legacy",
                "${workspaceFolder}\\Drivers\\CMSIS\\Device\\ST\\STM32F1xx\\Include",
                "${workspaceFolder}\\Drivers\\CMSIS\\Include"
            ],
            "defines": [
                "USE_HAL_DRIVER",
                "STM32F103xB"
            ],
            "compilerPath": "c:\\Program Files\\arm-gnu-toolchain-13.3.rel1-mingw-w64-i686-arm-none-eabi\\bin\\arm-none-eabi-gcc.exe",
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "gcc-arm"
        }
    ],
    "version": 4
}
```

![47_Configure_IntelliSense_text][47_Configure_IntelliSense]

Include paths and defines can be copied from "Makefile".

![48_Configure_IntelliSense_text][48_Configure_IntelliSense]
![49_Configure_IntelliSense_text][49_Configure_IntelliSense]

Now there are no false errors in the "Problems" panel.

![50_Configure_IntelliSense_text][50_Configure_IntelliSense]

### 5. Configure download and reset tasks.

Separate VSCode tasks must be created to download our program to the microcontroller and to reset the microcontroller. Add the following tasks to "\.vscode\tasks.json" file:

```
{
    "label": "openocd download",
    "type": "shell",
    "command": "openocd",
    "args":
    [
        "-f",
        "interface/stlink-dap.cfg",
        "-f",
        "target/stm32f1x.cfg",
        "-c",
        "program build/${command:makefile.getLaunchTargetFileName}.elf verify reset exit",
    ],
    "group":
    {
        "kind": "none",
        "isDefault": false
    },
    "dependsOn": "make build",
    "options":
    {
        "cwd": "${workspaceFolder}"
    },
    "problemMatcher": [],
},
{
    "label": "openocd reset",
    "type": "shell",
    "command": "openocd",
    "args":
    [
        "-f",
        "interface/stlink-dap.cfg",
        "-f",
        "target/stm32f1x.cfg",
        "-c",
        "init; reset; exit"
    ],
    "group":
    {
        "kind": "none",
        "isDefault": false
    },
    "options":
    {
        "cwd": "${workspaceFolder}"
    },
    "problemMatcher": [],
}
```

![51_Configure_download_and_reset_tasks_text][51_Configure_download_and_reset_tasks]

Now these custom tasks can be called to download our program to the microcontroller and to reset the microcontroller. Connect your debugger to your development board. Then connect the debugger to your PC's USB port.

![52_Configure_download_and_reset_tasks_text][52_Configure_download_and_reset_tasks]

Navigate to "View" -> "Command Palette...", type "Tasks: Run Task" and select "openocd download".

![53_Configure_download_and_reset_tasks_text][53_Configure_download_and_reset_tasks]

The program is downloaded to our microcontroller successfully.

![54_Configure_download_and_reset_tasks_text][54_Configure_download_and_reset_tasks]

<video controls muted src="video/Downloaded_program.mp4"></video>

### 6. Configure debugger.

VSCode's "Cortex-Debug" extension provides the ability to debug ARM Cortex-M microcontrollers. A separate launch configuration must be created to use the debugger.

Inside ".vscode" folder create a "launch.json" file with these contents:

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations":
    [
        {
            "name": "openocd debug",
            "type": "cortex-debug",
            "request": "launch",
            "servertype": "openocd",
            "configFiles":
            [
                "interface/stlink-dap.cfg",
                "target/stm32f1x.cfg"
            ],
            "searchDir": [],
            "executable": "build/${command:makefile.getLaunchTargetFileName}.elf",
            "svdFile": "STM32F103.svd",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "none",
            "liveWatch":
            {
                "enabled": true,
                "samplesPerSecond": 1
            },
            "preLaunchTask": "make build",
            "postDebugTask": "openocd reset",
            "cwd": "${workspaceFolder}"
        }
    ]
}
```

![55_Configure_debugger_text][55_Configure_debugger]

To start debugging navigate to "Run and Debug" panel and click the green "Play" button.

![56_Configure_debugger_text][56_Configure_debugger]

The debugger is launched successfully.

![57_Configure_debugger_text][57_Configure_debugger]




[Arm GNU Toolchain]: https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads
[MinGW-w64]: https://github.com/skeeto/w64devkit/releases
[OpenOCD]: https://github.com/openocd-org/openocd/releases
[STM32CubeMX]: https://www.st.com/en/development-tools/stm32cubemx.html#st-get-software
[ST-LINK driver]: https://www.st.com/en/development-tools/stsw-link009.html#get-software
[System View Description]: https://www.st.com/en/microcontrollers-microprocessors/stm32f103c8.html#cad-resources 
[VSCode]: https://code.visualstudio.com/
[C/C++ VSCode extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools
[Makefile Tools VSCode extensions]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.makefile-tools
[Cortex-Debug]: https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug
[Todo Tree]: https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree
[Doxygen Documentation Generator]: https://marketplace.visualstudio.com/items?itemName=cschlosser.doxdocgen


[1_Arm_GNU_Toolchain]: images/1_Arm_GNU_Toolchain.png
[2_Arm_GNU_Toolchain]: images/2_Arm_GNU_Toolchain.png
[3_Arm_GNU_Toolchain]: images/3_Arm_GNU_Toolchain.png
[4_MinGW_w64]: images/4_MinGW_w64.png
[5_MinGW_w64]: images/5_MinGW_w64.png
[6_MinGW_w64]: images/6_MinGW_w64.png
[7_OpenOCD]: images/7_OpenOCD.png
[8_OpenOCD]: images/8_OpenOCD.png
[9_OpenOCD]: images/9_OpenOCD.png
[10_STM32CubeMX]: images/10_STM32CubeMX.png
[11_ST_LINK_driver]: images/11_ST_LINK_driver.png
[12_System_View_Description]: images/12_System_View_Description.png
[13_System_View_Description]: images/13_System_View_Description.png
[14_System_View_Description]: images/14_System_View_Description.png
[15_Visual_Studio_Code]: images/15_Visual_Studio_Code.png
[16_C_VSCode_extension]: images/16_C_VSCode_extension.png
[17_Makefile_Tools_VSCode_extension]: images/17_Makefile_Tools_VSCode_extension.png
[18_Cortex_Debug_VSCode_extension]: images/18_Cortex_Debug_VSCode_extension.png
[19_Todo_Tree_VSCode_extension]: images/19_Todo_Tree_VSCode_extension.png
[20_Doxygen_Documentation_Generator_VSCode_extension]: images/20_Doxygen_Documentation_Generator_VSCode_extension.png
[21_Generate_code]: images/21_Generate_code.png
[22_Generate_code]: images/22_Generate_code.png
[23_Generate_code]: images/23_Generate_code.png
[24_Generate_code]: images/24_Generate_code.png
[25_Generate_code]: images/25_Generate_code.png
[26_Generate_code]: images/26_Generate_code.png
[27_Generate_code]: images/27_Generate_code.png
[28_Generate_code]: images/28_Generate_code.png
[29_Generate_code]: images/29_Generate_code.png
[30_Write_LED_driver]: images/30_Write_LED_driver.png
[31_Write_LED_driver]: images/31_Write_LED_driver.png
[32_Write_LED_driver]: images/32_Write_LED_driver.png
[33_Write_LED_driver]: images/33_Write_LED_driver.png
[34_Write_LED_driver]: images/34_Write_LED_driver.png
[35_Write_LED_driver]: images/35_Write_LED_driver.png
[36_Configure_build_tasks]: images/36_Configure_build_tasks.png
[37_Configure_build_tasks]: images/37_Configure_build_tasks.png
[38_Configure_build_tasks]: images/38_Configure_build_tasks.png
[39_Configure_build_tasks]: images/39_Configure_build_tasks.png
[40_Configure_build_tasks]: images/40_Configure_build_tasks.png
[41_Configure_build_tasks]: images/41_Configure_build_tasks.png
[42_Configure_build_tasks]: images/42_Configure_build_tasks.png
[43_Configure_build_tasks]: images/43_Configure_build_tasks.png
[44_Configure_build_tasks]: images/44_Configure_build_tasks.png
[45_Configure_build_tasks]: images/45_Configure_build_tasks.png
[46_Configure_IntelliSense]: images/46_Configure_IntelliSense.png
[47_Configure_IntelliSense]: images/47_Configure_IntelliSense.png
[48_Configure_IntelliSense]: images/48_Configure_IntelliSense.png
[49_Configure_IntelliSense]: images/49_Configure_IntelliSense.png
[50_Configure_IntelliSense]: images/50_Configure_IntelliSense.png
[51_Configure_download_and_reset_tasks]: images/51_Configure_download_and_reset_tasks.png
[52_Configure_download_and_reset_tasks]: images/52_Configure_download_and_reset_tasks.png
[53_Configure_download_and_reset_tasks]: images/53_Configure_download_and_reset_tasks.png
[54_Configure_download_and_reset_tasks]: images/54_Configure_download_and_reset_tasks.png
[55_Configure_debugger]: images/55_Configure_debugger.png
[56_Configure_debugger]: images/56_Configure_debugger.png
[57_Configure_debugger]: images/57_Configure_debugger.png