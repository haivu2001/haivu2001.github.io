---
layout: post
title:  "State Pattern could save your head."
date:   2021-04-04 16:17:46 +0700
categories: c++ game design pattern
---

This is how you and me have been doing to our heroes in some imaginary fighting game:

{% highlight cpp %}
void CPlayer::ProcessInput {
    if (pressed["GAMEPAD_CROSS"]) {
        ChangeSprite("slap");
        Slap();
    }
}
{% endhighlight %}

Press `X` on your gamepad to slap your foes. Wait... you might slap them again and again by just spamming `X` even when you have not stopped slapping.
You can see that the animation does not look realistic.
    
Here is a quick fix:

{% highlight cpp %}
bool slapping = false;

// Only slap when we are not slapping.
if (pressed["GAMEPAD_CROSS"] && !slapping) {
    slapping = true; // Remember that we are still slapping.
//...
}
{% endhighlight %}

Now let's add a `Charge` skill.

{% highlight cpp %}
if (pressed["GAMEPAD_CIRCLE"]) {
    power++;
}

if (released["GAMEPAD_CIRCLE"]) {
    power = 0;
    ChargedPunch();
}
{% endhighlight %}

Things look well at first. You will soon realize there is a way to cheat this game: Hold `Circle`, wait for an enemy, press 
`X` then release `Circle` immediately. He lost his focus when he was slapped, and you gave him a powerful punch which he would never
have been able to evade.

### How about State Pattern?

It saves your day.

{% highlight cpp %}
class State {
    virtual State* loop() = 0;
};

class StandingState {
    State* loop() {
        if (pressed["GAMEPAD_X"]) return new SlappingState;
        if (pressed["GAMEPAD_CIRCLE"]) return new ChargingState;
    } 
};

class SlappingState {
    State* loop() {
        if (FinishedSlapping) return new StandingState;
    }
};

class ChargingState {
    State* loop() {
        if (released["GAMEPAD_CIRCLE"]) {
            ChargedPunch();
            return new StandingState;
        }
    }
};
{% endhighlight %}

When you are in standing state, you can either press `X` to slap or `Circle` to punch your foes.
However, during slapping state, you can't do any input until slapping animation finishes. Same goes for charging state, you must release 
`Circle` to do a powerful punch before your hero becomes reponsive to other input.