---
description: Learn about the core systems of Open 3D Engine (O3DE) and how you can extend those systems by programming.
title: Open 3D Engine Programming Guide
linktitle: Programming
weight: 600
---

The *engine core* encompasses the source code, systems, and modules that underlie **Open 3D Engine (O3DE)** and its tools. All of these tools---**O3DE Editor**, **Asset Processor**, **Script Canvas**, and so on---work together to build an interactive 3D experience that uses modern rendering techniques and gameplay logic. Using these tools, you can take your design from an empty scene to a fully polished project that you can deploy and share. In this section, you'll gain a deeper understanding of each part of the engine core and learn how you can expand O3DE's toolkit.

## Related topics

| Topic | Description |
| --- | --- |
| [O3DE C++ Coding Standards](https://github.com/o3de/sig-core/blob/main/governance/Coding-Standards-and-Style-Guide.md) | If you're programming features to contibute to [o3de repository](https://github.com/o3de/o3de), follow the coding standards used throughout O3DE's C++ codebase. |

## Prerequisites

* C++17
* Python 3

The O3DE source code is written in C++, with several supporting tools written in Python. We recommend that you have fundamental knowledge of either C++ or Python programming to extend O3DE.


## Start here

Start by learning about the shared systems in the engine core by reading [Overview of the O3DE SDK](/docs/welcome-guide/key-concepts/#overview-of-the-o3de-sdk). 
In this topic, you'll learn how to navigate the O3DE directory structure and become familiar with the core modules in the O3DE SDK. The core modules are the entry points to all of the functionality in O3DE.


## Learning paths

Depending on the part of the engine that you want to develop, there are different learning tracks that you can follow. While each learning path may be unique to your case, the following topics can help get you started on some common development tasks:


### Develop a component
  
  - [Component Entity System (CES)](/docs/welcome-guide/key-concepts/#the-component-entity-system)
  
  - [Event Bus (EBus) system](/docs/user-guide/programming/ebus/)
  
  - [Programmer's Guide to Component Development](/docs/user-guide/programming/components/)


### Develop a Gem
  
  - [Gem Module system](/docs/user-guide/programming/gems/overview/)

  - [Create an O3DE Gem](/docs/user-guide/programming/gems/creating/)


### Develop Atom Renderer features
  
  - [Atom Renderer Developer Guide](/docs/atom-guide/dev-guide/)
