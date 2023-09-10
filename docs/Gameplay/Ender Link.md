---
title: Ender Link
---


# The Ender Link System

Sometimes you need to transfer items or fluids across large distances.  
The Ender Link system is one of the options for doing so. You can attach an Ender Link cover to an item or fluid
container and link it to an Ender Link network, using a controller.


## Building a Local Ender Link Network

The Ender Link controllers are the central component of your Ender Link network.  
You can connect any amount of covers to your controller, as long as you don't exceed its range.

Once you have created the controller multiblock, you can insert Ender Link cards into its card writer.
It will then write its own ID on the cards, which you need to insert into an Ender Link cover's card reader.


## Channels

Each Ender Link network has multiple channels, as well as a channel limit that depends on its tier.  
You can assign Ender Link covers to different channels to keep them separated from each other, while not needing to 
create an additional network (unless you exceed the channel limit).

Channels are not generally limited to transferring a single type(1) of resource.  
However, once it begins transferring anything, the channel will become locked to that resource type. The lock will
automatically be removed after no resources have been transferred for 2 seconds.
{ .annotate }

1. Items / Fluids by default. This may be expanded by addons.

!!! tip "Mixing Resource Types"
    In general, it is a good idea to not mix resource types on a channel, unless you are working within extremely tight
    channel limit constraints. In such situations, you must **manually** ensure that there is sufficient delay between 
    transferring different types.


## Expanding Your Network

Most of the time, the range of just one Ender Link controller will not be enough for your needs. This is where the
actual Ender Link **network** becomes relevant.

!!! info "All controllers on a network must share the same tier."

You can link multiple controllers together using Ender Link network connectors.  
Similarly to how the Ender Link cards are linked to a controller, network connectors are linked to an entire network.  
To link multiple controllers to a network, each of them needs to have a network connector with the same network ID in
its network connector slot.

Each controller that is added to the network (except for the initial one) will use two of the network's available 
channels. The remaining channels will behave just like they do for local networks.


## Interdimensional Transfer

Depending on the network's tier, you will gain the ability to even expand it across multiple dimensions.

When doing so, however, you need to supply power to one of the controllers on your network.  
The network connectors will also need to be replaced with special _cross-dimensional_ network connectors.