# HomeBot

HomeBot is a dynamic smart home control application built using Python and KivyMD. I attempted this project in high school to practice on kivymd and language parsing concepts i learnt from "Programming principles and concept using C++ by Bjarne Stroustrup". The core milestone I acheived in this project is implementing a custom **Data Definition Language (DDL)** designed to define the structure of a building (rooms and gadgets) dynamically, allowing the UI to render itself based on a text configuration string rather than hardcoded layouts.

## Project Overview

This project demonstrates a data-driven approach to UI generation. Instead of manually placing buttons and sliders for every light or fan, the application parses a custom configuration string to build the object model in memory, which the interface then reflects.

### Key Features

*   **Custom HomeBotDDL**: A specialized syntax for defining the hierarchy of a home.
*   **Dynamic UI Generation**: The application interface (House and Room cards) is constructed at runtime based on the parsed configuration.
*   **Gadget Types**: Supports two primary control modes:
    *   `switch`: Binary on/off control (e.g., lights).
    *   `regulate`: Percentage-based control (e.g., fans, dimmers).
*   **Hierarchical State Management**: Gadgets are aware of their parent rooms, allowing for group logic (e.g., checking if a whole room is "off").

### The HomeBot DDL

The configuration language uses specific keys to define objects. This string is parsed by `homebot_config.py`.

**Syntax Keys:**
*   `$N()`: **Name** of an object.
*   `$C()`: **Control** type (`switch` or `regulate`).
*   `$G()`: **Gadgets** list (used within a Room).
*   `[...]`: Denotes a **Room**.
*   `{...}`: Denotes a **Gadget**.

**Example Configuration:**
```text
[
    $N(Living Room)
    $G(
        {$N(Main Light) $C(switch)}
        {$N(Ceiling Fan) $C(regulate)}
    )
]
{$N(Porch Light) $C(switch)}
```

### Technical Stack

*   **Language**: Python
*   **Framework**: Kivy & KivyMD (Material Design)
*   **Architecture**:
    *   **Backend (`homebot_config.py`)**: Contains the lexer/parser logic for HomeBotDDL and the `Gadget`/`Room` class structures.
    *   **Frontend (`home_page.py`)**: Maps the parsed objects to KivyMD widgets (`HouseCard`, `RoomListItem`, custom switches/sliders).
    *   **Entry Point (`main.py`)**: Bootstraps the mobile-sized application window.

### Usage

1.  Ensure Kivy and KivyMD are installed.
2.  Run the application:
    ```bash
    pip install kivy kivymd
    python main.py
    ```