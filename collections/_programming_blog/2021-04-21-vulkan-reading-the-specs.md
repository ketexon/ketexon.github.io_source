---
layout: post
title: "Reading the Vulkan Specs so You Don't Have To"
date_published: 2021-04-21
updated: false
published: false
---
1. 
{:toc}

# Introduction

The [Vulkan specification]{:target="_blank"} defines how [Khronos's Vulkan API]{:target="_blank"} should function on all hardware devices. The specification itself for version 1.2.176 fits inside a 1230 page PDF, and all registered extensions to Vulkan add an extra 835 pages. It seems very intimidating trying to get into development with Vulkan, so this post serves the purpose of summarizing the core specifications and major extension specifications. Actually, I lied. This post is mainly to allow myself to document my understanding of Vulkan as I try to master it by reading the specifications. 

# What is Vulkan?

Vulkan is what is known as a graphics and computing API, which essentially means that it allows you to use the graphics card on a computer. This is especially useful for making graphical applications and abusing the high parallelism of the GPU to perform certain complex calculations faster than on a CPU. Vulkan is especially notable for its freedom, its explicitness, and its speed, succeeding the OpenGL API. Since it is solely a specification, it is able to be cross-platform, but you already know that Mac ruins the fun with its Metal API.

# Terminology

The Vulkan specs provide a [glossary]{:target="_blank"} for a lot of major terminology. Vulkan-specific terms will be italicized, as they are in the specifications.

# Execution Environment

## Overview

Vulkan gives the _host_ (computer) access to _devices_ (graphics cards being the notable type).

Each device exposes a set of _queues_, which handle the execution of commands (like an abstraction of a processor). Parallellism exists at this point of execution, since devices may have many queues which can accept and run commands asynchronously to other queues and to the computer. 

Queues may not all be able to do the same things (eg. a queue may not be able to encode video but it may be able to do computations), so queues are organized into _queue families_, each containing _compatible_ queues that can perform the same operations. These are useful since it does not really matter which queue runs the commands you send, as long as it can. 

To actually execute commands on these queues, a _command buffer_ is used, which represents a set of commands that are to be run in order. This can be thought of as an abstraction of assembly.

The device also exposes the memory it uses (either video memory or host memory), which may be explicitly used by the host.

## Queue Operations

Command buffers are recorded entirely before they are executed. They are then submitted in a _batch_ (collection of command buffers) to a queue via a _queue submission_ command, after which the commands will execute in a certain order.

_Queue operations_ are the operations represented by the command buffers (work) themselves and the semaphore operations. 

Synchronization with other commands can occur here with semaphores, which can be as simple boolean values that act as signals for when certain events happen (which could be the start of a command, the completion, etc.). Queues can wait on a semaphore to execute and signal a semaphore on completion/start.

[Vulkan specification]: https://www.khronos.org/registry/vulkan/specs/1.2-extensions/html/vkspec.html
[Khronos's Vulkan API]: https://www.khronos.org/vulkan/
[Vulkan Tutorial]: https://vulkan-tutorial.com/
[glossary]: https://renderdoc.org/vkspec_chunked/chap54.html#glossary