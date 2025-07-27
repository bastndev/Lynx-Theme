# Lynx Theme Pro Architecture

## Overview

**Lynx Theme Pro** is a comprehensive extension for Visual Studio Code that provides multiple color themes and a custom icon system. The extension is designed to enhance the development experience with visually appealing and eye-friendly themes, along with intuitive `icons` for different file and folder types.

## How it Works

When a user activates the **Lynx Theme Pro** extension in VS Code:

1. The `package.json` file registers the themes and icons through the `contributes` field.
2. Based on user settings or interactions, the **Theme Engine** or **Icon Theme Engine** loads the respective JSON configurations.
3. These configurations are interpreted by the VS Code host and applied to the **User Interface**.
4. Supporting files like icons (SVGs) and documentation provide both visual fidelity and development support.

> 💡 **Note on naming conventions:**  
> Color themes use a prefix (`Lynx-`) followed by a sorting letter (`x`, `y`, `z`) to control display order in the VS Code UI. For example:  
> `Lynx-xGhibli-theme.json`, `Lynx-yCoffee-theme.json`, `Lynx-zKiro-theme.json`.

---

## Architecture Diagram

```mermaid
graph TB
    subgraph "📦 Lynx Theme Pro Extension"
        direction TB
        A[package.json<br/>📋 Main Configuration]
        
        subgraph "🔧 Core Structure"
            direction LR
            B[Contributes] --> C[🎨 Themes]
            B --> D[🎯 Icon Themes]
        end
        
        subgraph "🎨 Color Themes Collection"
            direction TB
            E[Lynx-Dark-theme.json<br/>🌙 Dark Theme]
            F[Lynx-Light-theme.json<br/>☀️ Light Theme]
            G[Lynx-Night-theme.json<br/>🌃 Night Theme]
            H[Lynx-xGhibli-theme.json<br/>🌸 Ghibli Theme]
            I[Lynx-yCoffee-theme.json<br/>☕ Coffee Theme]
            J[Lynx-zKiro-theme.json<br/>🤖 Kiro Theme]
        end
        
        subgraph "🎯 Icon System"
            direction TB
            K[lynx-icons.json<br/>📁 Icon Configuration]
            L[assets/icons/<br/>🎨 SVG Collection]
            
            subgraph "📦 Icon Categories"
                direction LR
                M[📄 File Icons<br/>500+ types]
                N[📁 Folder Icons<br/>100+ variants]
                O[🔧 Special Icons<br/>Specialized]
            end
        end
        
        subgraph "📚 Documentation & Resources"
            direction LR
            P[README.md<br/>📖 Documentation]
            Q[CONTRIBUTING.md<br/>🤝 Guide]
            R[assets/images/<br/>🖼️ Resources]
            S[CHANGELOG.md<br/>📝 History]
        end
    end
    
    subgraph "🎯 VS Code Integration Layer"
        direction TB
        T[VS Code Extension Host<br/>🏠 Runtime Environment]
        
        subgraph "⚙️ Engine Systems"
            direction LR
            U[Theme Engine<br/>🎨 Color Processing]
            V[Icon Theme Engine<br/>📁 Icon Processing]
        end
        
        W[User Interface<br/>👤 Visual Output]
    end
    
    %% Main connections
    A --> B
    C --> E
    C --> F
    C --> G
    C --> H
    C --> I
    C --> J
    D --> K
    K --> L
    L --> M
    L --> N
    L --> O
    
    %% Integration connections
    A -.-> T
    E -.-> U
    F -.-> U
    G -.-> U
    H -.-> U
    I -.-> U
    J -.-> U
    K -.-> V
    U --> W
    V --> W
    T --> U
    T --> V
    
    %% Styling
    classDef mainConfig fill:#ff6b6b,stroke:#333,stroke-width:2px,color:#fff
    classDef themes fill:#4ecdc4,stroke:#333,stroke-width:2px,color:#fff
    classDef icons fill:#45b7d1,stroke:#333,stroke-width:2px,color:#fff
    classDef engine fill:#96ceb4,stroke:#333,stroke-width:2px,color:#fff
    classDef output fill:#feca57,stroke:#333,stroke-width:2px,color:#000
    classDef docs fill:#a8e6cf,stroke:#333,stroke-width:2px,color:#000
    
    class A mainConfig
    class C,E,F,G,H,I,J themes
    class D,K,L,M,N,O icons
    class U,V engine
    class W output
    class P,Q,R,S docs

```