
Before going through this tutorial, it’s best to watch the Speech-Machine for Animators video first, so you’ll know how animators are going to use it.


Also it would be helpful to fully read the Requirements page on this website.

This tutorial shows the step-by-step process how to set it up. To see that in action, watch the Speech-Machine for Riggers video.

The Setup process of the Speech-Machine is mapping the controls in your rig to the Containers. During this process you are working with the tool similar to how animators are working with it – the character rig needs to be referenced in scene, and at the top of the UI the namespace needs to be specified by selecting any control and clicking Set from Selected at the top of the UI.

This has the advantage that later even animators can make adjustments to the settings on the Setup Node and send back to rigging to update it in the rig.

## Setup Node
First we need to understand how the Setup Node works. The Setup Node is called __speechMachineSetup__ and it’s a simple transform node with tons of float and string attributes.

Never adjust those attributes directly, unless you are absolutely sure of what you are doing. The way to adjust those attributes is by going to the Setup Jaw/Lips/Tongue tab and from top to bottom fill and calibrate the fields.


## Titles Attach Transform
In the Setup Jaw/Lips/Tongue tab at the top you can find Titles Attach Transform.


Here you specify the transform where the subtitles are being attached to and where they are located. This won’t have any impact to the end result, but I recommend to specify it properly, so the titles are appearing nicely above the head.

Simply select the head control for example, click the 3 dots button next to Titles Attach Transform and click Set Transform from Selected.

This will create and select a plane called NAMESPACE::TitlesGuide. Move it so it’s located above the head.

You might notice that in the UI the field on the right side has some some confusing looking numbers and it’s changing as you move the planes.
This is just a mirror to an attribute in the Setup Node which is storing the offset matrix of the plane relative to the transform that you specified.

Later, if the Subtitles appear too big or too small, simply adjust the plane.

## Jaw Container
The first 3 lines are the most important


Select your jaw control attribute while it is in default pose (should be closed), click the 3 dots button next to Jaw Ctrl and in the dropdown menu that appears click Set From Selected.

Now we need to specify the jaw in the open pose. Simply pose the jaw, click the 3 dots button next to Jaw Pose and in the appearing drop down menu click Set Current Pose.

Then play with the Jaw Open Test slider below. If the jaw opens and closes correctly, it worked.

And then set the jaw percentages of where the jaw should be on the S (Jaw % for S) and TH (Jaw % for TH) sounds.
For the S, just make sure the tip of the teeth are meeting. In most rigs that would be 0 %. And for TH, just make sure the gap between the teeth is wide enough so the tip of the tongue has space to go inbetween.

## Other Containers
Before moving further, let’s make sure we know what exactly a Container is. The speech-machine has those containers:

- **Jaw** – we’ve done this already above
- **CornerInOut** – In the UI they are split into CornerIn, CornerOut
- **UpperUp** – Upperlip Raiser
- **LowerDown** – Lowerlip Depressor
- **Funnel** – SH, RR – Lips going forward
- **Puff** - for longer and harder P – lips pressing and cheeks puffing slightly
- **MouthClose** – lips closing, also when jaw is open
- **lower FFF** – bottom lips touching the teeth
- **Zipper**
- **Tongue Up** – N, L, T, D
- **Tongue TH** – The typical English sound TH
- **Tongue Back** – K, G

- Internally the Speech Machine is calculating an animation for each container. What we have to do with the UI is mapping our controls to the containers. And we already did one – the jaw.

While the simple containers (like the Jaw, UpperUp, LowerDown) just have a Ctrls field and a Pose field, some have 2 Pose fields (MouthClose, lower FFF, all the Tongue Containers). One for when Jaw is at default, and one for when jaw is open. They all need to be set properly.

## Multiple Control usage
In most cases, each control attribute in the rig should not be used more than once.

For example if you have a control attribute upper_ctrl.translateY that you specify for the upperUp container and for the mouthClosed container at the same time, you will immediately get a warning.

But the tool will still work, except that the result will be baked keys instead of clean keys. If you are ok with this, then don’t worry and feel free to use controls more than once.

Actually for the tongue this could be acceptable in many cases since animators are more likely not going to need to adjust the tongue animation.

One exception is the cornerIn and cornerOut containers. You can have a control that will get negative values from the cornerIn container, and positive values from the cornerOut container. Because those containers under the hood are actually combined into one container.

Another exception is the Puff Container. Since internally this is more like a post effect, it can handle it if there are already extisting control attributes defined here.

## Finish the Setup
Now that you know what containers are and how they work – let’s from top to bottom and map the Ctrls and Poses for each container.

Always remember to use the test sliders to see if things are set correctly!

## Bringing the setup node into the rig
When you are done mapping and calibrating your controls, simply duplicate the setup node, so it’s just named speechMachineSetup without namespace, and import that into your rig.

So next time you reference your rig, this node gets reference with the correct namespace

Also make sure you only have that node in the rig only once to avoid clashing names.

## Kangaroo Builder
If you are using Kangaroo Builder, you can click the Fill Commands with Setup Node button to store the settings. And when you rebuild the rig, the setup node is created automatically.

You can find an example to it in the MOUTH character inside the template project.