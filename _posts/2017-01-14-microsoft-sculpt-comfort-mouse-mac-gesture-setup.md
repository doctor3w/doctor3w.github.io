---
title: Microsoft Sculpt Comfort Mouse Mac Gesture Setup
comments: true
layout: post
type: text
description: A How-To on my custom Microsoft Sculpt Comfort Mouse setup for Macs using Karabiner.
---

UPDATE: A newer version of this for macOS El Captian and above can be found [here]().

I was looking for a nice Bluetooth mouse a while back and I came across the Microsoft Sculpt Comfort Mouse. It connected purely through Bluetooth and not an excessive USB wireless receiver. I found some other mice while looking around, but to me the Sculpt Comfort mouse looked the cleanest, and I could confirm it would work with a Mac from online reviews. You can find the mouse here: [Microsoft Sculpt Comfort Mouse](https://www.microsoft.com/accessories/en-us/products/mice/sculpt-comfort-mouse/h3s-00003).

After mulling it over for a while, I finally decided to bite the bullet and buy the mouse. The only thing that I left unknown when hitting that buy button was: What will I do with the side Windows button? I thought the gesture button on the side of the mouse could be easily configured to be shortcuts in the Mac preferences and boy was I wrong. Eventually I came across a solution. 

#### Karabiner
Karabiner is an open source application that remaps keys from keyboard input (avaiable here: [Karabiner](https://github.com/tekezo/Karabiner)). This is the perfect solution to solving the Sculpt Comfort special key input. Using the EventViewer application found under Karabiner's Misc & Uninstall section, you can see the different key inputs as you press/swipe the Windows button: 

![](/img/msmouse/eventviewer.png)

Now that we know the key codes for each key press/swipe, we can plug those into the `private.xml` file found in Karabiner's Misc & Uninstall section. Opening that up we will want to paste the code from below. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
  <devicevendordef>
    <vendorname>MICROSOFT</vendorname>
    <vendorid>0x045e</vendorid>
  </devicevendordef>
  <deviceproductdef>
    <productname>MICROSOFT_SCULPT_MOUSE</productname>
    <productid>0x07a2</productid>
  </deviceproductdef>
  <item>
    <name>Microsoft Sculpt Mouse - Map Windows Button</name>
    <identifier>private.msft_sculpt</identifier>
    <device_only>
        DeviceVendor::MICROSOFT, 
        DeviceProduct::MICROSOFT_SCULPT_MOUSE
    </device_only>
    <autogen>
        __KeyToKey__
        KeyCode::CONTROL_L,
        KeyCode::VK_NONE,
        ModifierFlag::NONE
    </autogen>
    <autogen>
        __KeyOverlaidModifier__
        KeyCode::COMMAND_L,
        KeyCode::COMMAND_L,
        KeyCode::LAUNCHPAD
    </autogen>
    <autogen>
        __KeyToKey__
        KeyCode::DELETE,
        ModifierFlag::COMMAND_L,
        KeyCode::MISSION_CONTROL
    </autogen>
    <autogen>
        __KeyToKey__
        KeyCode::TAB,
        ModifierFlag::COMMAND_L,
        KeyCode::CURSOR_DOWN,
        ModifierFlag::CONTROL_L
    </autogen>
    <autogen>
        __ScrollWheelToKey__
        ScrollWheel::LEFT,
        ModifierFlag::COMMAND_L,
        KeyCode::CURSOR_LEFT,
        ModifierFlag::CONTROL_L
    </autogen>
    <autogen>
        __ScrollWheelToKey__
        ScrollWheel::RIGHT,
        ModifierFlag::COMMAND_L,
        KeyCode::CURSOR_RIGHT,
        ModifierFlag::CONTROL_L
    </autogen>
    <autogen>
        __FlipScrollWheel__
        Option::FLIPSCROLLWHEEL_VERTICAL,
        Option::FLIPSCROLLWHEEL_HORIZONTAL
    </autogen>
  </item>
</root>
```

This XML code will map the Windows button to a few things: 

- Press ==> **Launchpad**
- Swipe up ==> **Mission Control**
- Swipe down ==> **Exposé**
- Press + Scroll Wheel Left ==> **Spaces Left**
- Press + Scroll Wheel Right ==> **Spaces Right**

These are completely customizable to your liking, but these felt most natural to me. Once the file has been saved, return to Karabiner, go to the tab Change Key and click Reload XML. Then an option should appear like below, check it off. 

![](/img/msmouse/changekey.png)

After doing so your new mouse should be setup to work with your Mac, swiping an all. Now you don't have to feel bad about not using the great swipe gestures on your trackpad. 